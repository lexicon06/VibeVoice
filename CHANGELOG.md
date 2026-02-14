# Changelog

## Changes Made

### Setup & Installation
- Created `requirements.txt` with all dependencies
- Created virtual environment `virt/` with CUDA-enabled PyTorch
- Added `RUN_GUIDE.md` with setup instructions

### Performance Optimizations
- Added CUDA optimizations (TF32, cudnn benchmark) in `demo/web/app.py`
- Default inference steps reduced from 5 to 3 for faster generation
- Default CFG scale set to 1.5
- Added float32 matmul precision optimization

### Engram-Inspired Optimizations (O(1) Lookups)
- **Text Cache**: Stores previously generated audio in memory
  - O(1) hash lookup for repeated text (same text + voice + settings)
  - LRU eviction when cache is full (max 100 entries)
  - Cache hits/misses tracked in logs
  - First generation saves audio to cache, subsequent plays are instant

### UI Improvements
- Added **Buffer slider** (0.1s - 3.0s) to control pre-buffering
  - Higher buffer = more audio buffered before playback = less stuttering
  - Default: 1.0s
- Updated default steps from 5 to 3
- Updated reset button to reflect new defaults

### Troubleshooting
- Added FlashAttention fallback to SDPA
- Fixed transformers version to 4.51.3 for compatibility

## Recommended Settings for Best Performance

### For smooth playback (reduce stuttering):
- **Buffer: 2-3 seconds** - buffers more audio before playing
- **Steps: 3** - good balance of speed/quality
- **CFG: 1.0-1.2** - lower = faster generation

### For best quality (may stutter):
- **Buffer: 0.1-0.5 seconds** - starts playing faster
- **Steps: 5-10** - better audio quality
- **CFG: 1.5** - standard quality

## Known Limitations

- This is a diffusion-based TTS model - inherently slower than non-diffusion TTS
- Requires powerful GPU (RTX 4060 can do ~5-10 it/s)
- Stuttering is due to GPU limitations, not software
- FlashAttention not available on Windows without CUDA toolkit compilation
