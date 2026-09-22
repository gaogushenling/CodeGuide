---
title: 第3-11节：视频生成——本地ffmpeg兜底机制
pay: https://t.zsxq.com/Ebkb0
---

# 《WaLiOffice - AI Agent 智能办公平台》第3-11节：视频生成——本地ffmpeg兜底机制

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、前言

大家好，我是技术UP主小傅哥。

上一节我们把远程视频链路做成了“7 个失败出口全部汇入 `local_video_artifact`”——远程是首选，本地是底线。但当时 `local_video::generate_local_video` 只是个名字，这节打开这个黑盒：**不调用任何 AI 模型、不发任何网络请求，怎么在用户本机上“无中生有”合成一段能播放的 MP4？**

先说结论：WaLiOffice 的本地兜底**不是**“ffmpeg 滤镜拼一张静态图”，而是一条自绘渲染管线：

> **纯 Rust Canvas 逐像素光栅化 → PPM 帧序列 → ffmpeg 编码封装 MP4（含占位音轨）**。场景也不是随机的——太阳公转、丝带流动、卫星环绕、甚至**用户话题里出现“猫”就画一只摇尾巴追蝴蝶的猫**。AI 挂了，兜底依然“看得懂需求”。

## 一、本章诉求

1. **理解兜底管线分层**：帧生成（Rust 计算）与视频封装（ffmpeg 进程）职责分离，为什么这样分
2. **掌握 Canvas 软件光栅化**：像素缓冲、alpha 混合、渐变/圆/椭圆/三角/线条的逐像素实现
3. **掌握 PPM 最简图像格式**：6 字节头 + 裸 RGB，为什么中间帧选它
4. **理解分辨率上限、帧数钳制（3-8 秒）、偶数对齐（yuv420p 硬约束）
5. **掌握 ffmpeg 编码命令逐参数**：framerate/lavfi 音轨/volume/afade/libx264/yuv420p/faststart/shortest
6. **理解内容感知兜底**：topic 关键词切换场景（猫彩蛋），兜底不是死板的占位图
7. **理解产物落位**：outputs/videos/{uuid}/ 静态服务 + 中间帧清理

## 二、流程设计

### 2.1 本地兜底渲染管线

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walioffice/walioffice-3-11-01.png" width="950px">
</div>

```
local_video_artifact()（3-10 的 7 个失败出口之一触发）
    ↓
① ensure_ffmpeg_available()：ffmpeg -version 探测
   没有？→ Err（与远程失败原因合并报错，兜底也有底线）
    ↓
② 建渲染目录：{render_output_dir}/videos/{uuid}/frames/
   （render_output_dir 来自 AIPPT_RENDER_OUTPUT_DIR，默认 outputs）
    ↓
③ 规格收敛：
   (w,h) = local_dimensions()   // 按比例封顶：9:16→540×960，默认→960×540
   frame_count = num_frames.clamp(frame_rate×3, frame_rate×8)  // 3~8 秒
    ↓
④ 逐帧循环（72~192 帧）：
   Canvas::new(w, h) → draw_scene(canvas, topic, progress) → frame_%04d.ppm
    ↓
⑤ encode_video()：ffmpeg 子进程
   frame_%04d.ppm + sine 音轨(523Hz) → libx264/yuv420p → video.mp4
    ↓
⑥ 清理 frames/ 中间帧，保留 video.mp4
    ↓
LocalVideoOutput { public_url: "/outputs/videos/{uuid}/video.mp4",
                   file_path, seconds, size, frame_count }
    ↓
ServeDir("/outputs") 静态服务 → 前端 <video> 直接播放
```
