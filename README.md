# Swin2SR Video Super-Resolution (2x)

This repository provides a complete pipeline to enhance video quality using the **Swin2SR (SwinV2-based Image Super-Resolution)** model. It is specifically designed to upscale low-resolution videos (like CCTV footage) by a factor of 2 while maintaining high fidelity and avoiding memory constraints through tiled processing.

---

## 🔗 Interactive Demo (Synchronized Playback)

👉 **Live GitHub Pages Demo:**  
https://athithyakrishnaa.github.io/2X-Swin2SR-VideoEnhancer/

This interactive demo allows you to:
- ▶️ Play **original and enhanced videos simultaneously**
- ⏸ Pause both videos together
- Visually compare **frame-level improvements** from Swin2SR ×2
- Observe detail recovery in low-resolution CCTV footage

> **Note:** Videos in the demo are resized for web preview and layout consistency.  
> Full-resolution enhanced outputs are preserved in the actual result files.

---

## Features

* **2x Upscaling**: Efficiently doubles the resolution of input video frames.
* **Tiled Processing**: Implements a sliding window (tiled) approach to process high-resolution frames without running out of GPU memory (OOM).
* **Full Video Pipeline**: Automates the process from video frame extraction to final video reconstruction.
* **Side-by-Side Comparison**: Built-in HTML visualization to compare original and enhanced videos directly in the browser.

---

## How It Works

The system follows a sequential pipeline to transform a low-quality video into an enhanced version:

1. **Frame Extraction**: Uses OpenCV to split the input video into individual PNG frames.
2. **AI Enhancement**: Each frame is passed through the Swin2SR model for super-resolution.
3. **Video Reconstruction**: The enhanced frames are compiled back into a high-definition `.mp4` video file.

---

## Model Details

* **Model Name**: `caidas/swin2SR-lightweight-x2-64`
* **Architecture**: Swin2SR (Swin Transformer V2 for Image Super-Resolution).
* **Type**: Lightweight version optimized for speed and efficiency while maintaining competitive performance.
* **Pre-trained weights**: Hosted on Hugging Face.

---

## Installation

To run this project, ensure you have the following dependencies installed:

```bash
pip install transformers accelerate

```

---

## Workflow

### 1. Initialization

The project loads the `Swin2SRForImageSuperResolution` model and its corresponding processor from the Hugging Face Hub. It automatically detects and utilizes a GPU (CUDA) if available for faster processing.

### 2. Video Input

The pipeline allows users to upload a video file (e.g., `cctv.mp4`). This file is then processed to extract frames at its original FPS.

### 3. Tiled Enhancement

To handle potentially large resolutions, the code implements an `enhance_tiled` function:

* **Tile Size**: 256x256 pixels.
* **Overlap**: 32 pixels to ensure seamless stitching and avoid edge artifacts.
* **Process**: It crops the frame into tiles, enhances each tile independently, and pastes them back into a new image with 2x dimensions.

### 4. Output

The final enhanced video is saved as `enhanced_video.mp4` using the `mp4v` codec.

---
