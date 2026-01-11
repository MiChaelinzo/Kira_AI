# Kira AI - Detailed Installation Guide

This guide provides detailed installation instructions for all platforms, with special focus on resolving common build issues.

## Table of Contents
- [Windows Installation](#windows-installation)
- [macOS Installation](#macos-installation)
- [Linux Installation](#linux-installation)
- [Troubleshooting](#troubleshooting)

---

## Windows Installation

### Prerequisites

#### 1. Install Python 3.10+
1. Download Python from [python.org](https://www.python.org/downloads/)
2. **IMPORTANT**: Check "Add Python to PATH" during installation
3. Verify: Open Command Prompt and run `python --version`

#### 2. Install Visual Studio Build Tools (REQUIRED for llama-cpp-python)
This is the most common source of installation errors on Windows.

1. Download [Visual Studio Build Tools 2022](https://visualstudio.microsoft.com/downloads/)
   - Scroll down to "Tools for Visual Studio"
   - Download "Build Tools for Visual Studio 2022"

2. Run the installer and select **"Desktop development with C++"** workload

3. Ensure these components are selected:
   - ✅ MSVC v143 - VS 2022 C++ x64/x86 build tools
   - ✅ Windows 11 SDK (or Windows 10 SDK)
   - ✅ C++ CMake tools for Windows

4. Complete the installation (may take 10-20 minutes)

5. **RESTART your computer** or at minimum open a NEW terminal

### Installing Dependencies

#### Option A: CPU-only Installation (Simplest)
```cmd
pip install llama-cpp-python
pip install -r requirements.txt
```

#### Option B: Pre-built Wheels (Fast, No Compilation)
```cmd
pip install llama-cpp-python --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cpu
pip install -r requirements.txt
```

#### Option C: NVIDIA CUDA/GPU Support (Recommended for GPU users)
```cmd
set CMAKE_ARGS=-DGGML_CUDA=on
set FORCE_CMAKE=1
pip install llama-cpp-python --force-reinstall --no-cache-dir
pip install -r requirements.txt
```

For CUDA 12.x specifically:
```cmd
set CMAKE_ARGS=-DGGML_CUDA=on -DCMAKE_CUDA_ARCHITECTURES=all-major
pip install llama-cpp-python --force-reinstall --no-cache-dir
```

### Model Setup

1. Create a `models` folder in your Kira directory
2. Download a compatible GGUF model:
   - **Phi-3-mini-4k-instruct-fp16.gguf** (Recommended, ~7GB): [Download](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-gguf)
   - **Phi-3-mini-4k-instruct-q4.gguf** (Smaller, ~2.4GB): [Download](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-gguf)
3. Place the model file in the `models` folder
4. Update your `.env` file:
   ```
   LLM_MODEL_PATH=models/Phi-3-mini-4k-instruct-fp16.gguf
   ```

---

## macOS Installation

### Prerequisites
```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install dependencies
brew install cmake python@3.11

# For Apple Silicon (M1/M2/M3), Metal support is automatic
```

### Installing Dependencies
```bash
pip3 install -r requirements.txt
```

For Apple Silicon with Metal acceleration:
```bash
CMAKE_ARGS="-DGGML_METAL=on" pip3 install llama-cpp-python --force-reinstall --no-cache-dir
pip3 install -r requirements.txt
```

---

## Linux Installation

### Prerequisites
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip cmake build-essential portaudio19-dev

# Fedora
sudo dnf install python3 python3-pip cmake gcc-c++ portaudio-devel

# Arch
sudo pacman -S python python-pip cmake base-devel portaudio
```

### Installing Dependencies
```bash
pip3 install -r requirements.txt
```

For NVIDIA CUDA support:
```bash
CMAKE_ARGS="-DGGML_CUDA=on" pip3 install llama-cpp-python --force-reinstall --no-cache-dir
pip3 install -r requirements.txt
```

---

## Troubleshooting

### "CMAKE_C_COMPILER not set" / "nmake not found" (Windows)
**Cause**: Visual Studio Build Tools not installed or not in PATH

**Solution**:
1. Install Visual Studio Build Tools 2022 with "Desktop development with C++" workload
2. **Open a NEW terminal** after installation
3. Retry the pip install

### "Building wheel for llama-cpp-python failed"
**Solution 1**: Use pre-built wheels
```bash
pip install llama-cpp-python --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cpu
```

**Solution 2**: Force CMake and reinstall
```bash
# Windows
set FORCE_CMAKE=1
pip install llama-cpp-python --force-reinstall --no-cache-dir

# Linux/macOS
FORCE_CMAKE=1 pip install llama-cpp-python --force-reinstall --no-cache-dir
```

### "No module named 'llama_cpp'"
**Cause**: llama-cpp-python not installed correctly

**Solution**: Reinstall with verbose output to see errors:
```bash
pip install llama-cpp-python -v
```

### PyAudio Installation Issues

**Windows**:
```bash
pip install pipwin
pipwin install pyaudio
```

**macOS**:
```bash
brew install portaudio
pip install pyaudio
```

**Linux**:
```bash
sudo apt install portaudio19-dev
pip install pyaudio
```

### CUDA Not Detected
1. Ensure NVIDIA drivers are installed
2. Install CUDA Toolkit from [NVIDIA](https://developer.nvidia.com/cuda-downloads)
3. Verify with: `nvidia-smi`
4. Reinstall llama-cpp-python with CUDA flags

### Model Loading Errors
1. Verify the model file exists in the correct path
2. Check the model format (must be .gguf)
3. Ensure sufficient RAM/VRAM for the model size
4. Try a smaller quantized model (q4 instead of fp16)

---

## Supported Models

Kira AI supports any GGUF format model compatible with llama-cpp-python:

| Model | Size | VRAM Required | Quality |
|-------|------|---------------|---------|
| Phi-3-mini-4k-instruct-fp16.gguf | ~7GB | 8GB+ | Best |
| Phi-3-mini-4k-instruct-q8.gguf | ~4GB | 6GB+ | Great |
| Phi-3-mini-4k-instruct-q4.gguf | ~2.4GB | 4GB+ | Good |
| Llama-3.2-3B-Instruct-Q4_K_M.gguf | ~2GB | 4GB+ | Good |

---

## Getting Help

If you're still having issues:
1. Check the [GitHub Issues](https://github.com/MiChaelinzo/Kira_AI/issues) for similar problems
2. Create a new issue with:
   - Your operating system and version
   - Python version (`python --version`)
   - Full error message
   - Steps you've tried
