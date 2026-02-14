# VibeVoice Setup Guide

## Prerequisites

- Python 3.9+
- NVIDIA GPU with CUDA support (recommended)
- Windows

## Quick Start (with venv)

```bash
# Create virtual environment
python -m venv virt

# Activate venv
virt\Scripts\activate.bat

# Install PyTorch with CUDA
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124

# Install transformers (required version)
pip install transformers==4.51.3

# Install remaining dependencies
pip install accelerate diffusers librosa gradio av aiortc uvicorn fastapi pydub soundfile scipy numba llvmlite

# Install vibevoice package
pip install -e .
```

## Run the Server

```bash
# With CUDA (recommended)
python demo\vibevoice_realtime_demo.py --port 8080 --device cuda

# Or with CPU (slower)
python demo\vibevoice_realtime_demo.py --port 8080 --device cpu
```

## Alternative: Run Directly with venv Python

```bash
virt\Scripts\python.exe demo\vibevoice_realtime_demo.py --port 8080 --device cuda
```

## Usage

1. Open browser: `http://localhost:8080`
2. Enter text
3. Select voice (e.g., en-Carter_man)
4. Click "Start"

## Troubleshooting

- **Port in use**: Use `--port 8080` or another port
- **CUDA not found**: Install CUDA PyTorch: `pip install torch --index-url https://download.pytorch.org/whl/cu124`
- **Module errors**: Make sure venv is activated

## Notes

- Default model: `microsoft/VibeVoice-Realtime-0.5B`
- Voice presets in: `demo\voices\streaming_model\`
- Uses SDPA attention (fallback when FlashAttention not available)
