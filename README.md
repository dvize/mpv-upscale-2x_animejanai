# mpv-upscale

## Overview
This project provides a PowerShell script (Windows only) to set up mpv to run ONNX upscaling models in realtime with TensorRT. Originally intented to use the 2x_AnimeJaNai models but any provided ONNX model can be selected during setup. 

## Installer Instructions
1. Download [`install.ps1`](https://github.com/the-database/mpv-upscale/releases/latest/download/install.ps1) from [Releases](https://github.com/the-database/mpv-upscale/releases)
2. Download ONNX models and move to same directory as `install.ps1`
3. Run Powershell with Admin rights, navigate to directory containing `install.ps1`, execute installer with commands: 
   ```
   Set-ExecutionPolicy unrestricted
   .\install.ps1
   ```
## 2x_AnimeJaNai Model
2x_AnimeJaNai is a realtime 2x model intended for high or medium quality 1080p anime with an emphasis on correcting the inherit blurriness of anime while preserving details and colors. It is not suitable for artifact-heavy or highly compressed content as it will just sharpen artifacts. The model also works with SD anime by running the model twice. The installer in this repository can set this model up to run with mpv on Windows.

Minimum of RTX 3080 is recommended for running UltraCompact model on 1080p in realtime; RTX 4090 is required to run Compact on 1080p in realtime. SuperUltraCompact should run in realtime on 1080p on some lower cards. The compact model is recommended on SD content. 

Samples: https://imgsli.com/MTUxMDYx
Comparisons to Anime4K + other compact models and upscalers: https://imgsli.com/MTUxMjMx 

## Manual Setup Instructions
If the installer cannot be used, setup can be done manually as follows. 
1. Install latest Python 3.10.x from https://www.python.org/downloads/windows/
1. Install latest Vapoursynth64 from https://github.com/vapoursynth/vapoursynth/releases
2. Install latest pre-release vs-mlrt from https://github.com/AmusementClub/vs-mlrt/releases
   1. Download vsmlrt-windows-x64-cuda.v12.7z and extract contents to `%APPDATA%\VapourSynth\plugins64`
3. Download ONNX model and move to `%APPDATA%\VapourSynth\plugins64\vsmlrt-cuda`
4. Run command, replacing {MODEL_NAME} with the name of the ONNX model: ```.\trtexec --fp16 --onnx={MODEL_NAME}.onnx --minShapes=input:1x3x8x8 --optShapes=input:1x3x1080x1920 --maxShapes=input:1x3x1080x1920 --saveEngine={MODEL_NAME}.engine --tacticSources=+CUDNN,-CUBLAS,-CUBLAS_LT```
5. Download latest beta mpv.net from https://github.com/mpvnet-player/mpv.net/releases
   1. Extract to a permanent location such as `C:\`
   2. Run `mpvnet.exe` once and then close it
7. Download contents of this repository and extract to `%APPDATA%\mpv.net`
