# Compiling Inference Engines for LLM Deployment on Huawei Kunpeng 920

This document provides detailed instructions on how to compile various inference engines for efficient deployment of large language models (LLMs) on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [ChatGLM.cpp Compilation](#3-chatglmcpp-compilation)
4. [Qwen.cpp Compilation](#4-qwencpp-compilation)
5. [llama.cpp Compilation](#5-llamacpp-compilation)
6. [Optimizing Compilation for Kunpeng 920](#6-optimizing-compilation-for-kunpeng-920)
7. [Troubleshooting Common Issues](#7-troubleshooting-common-issues)

## 1. Introduction

Compiling inference engines is a crucial step in deploying LLMs efficiently. Custom-built inference engines can take advantage of specific hardware features and optimizations, leading to better performance on platforms like the Huawei Kunpeng 920.

## 2. Prerequisites

Before proceeding, ensure you have the following installed:

- GCC/G++ (version 7.5.0 or higher recommended)
- CMake (version 3.18 or higher)
- Make
- Git
- Python 3.8+ with development headers

You can install these on Ubuntu-based systems with:

```bash
sudo apt-get update
sudo apt-get install build-essential cmake git python3-dev
```

Ensure you have the latest CMake:

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.28.1/cmake-3.28.1-linux-aarch64.sh
chmod +x cmake-3.28.1-linux-aarch64.sh
sudo mkdir -p /opt/cmake
sudo ./cmake-3.28.1-linux-aarch64.sh --prefix=/opt/cmake --skip-license
export PATH=/opt/cmake/bin:$PATH
echo "export PATH=/opt/cmake/bin:$PATH" >> ~/.bashrc
```

## 3. ChatGLM.cpp Compilation

To compile ChatGLM.cpp:

```bash
git clone --recursive https://github.com/li-plus/chatglm.cpp.git
cd chatglm.cpp
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

If you encounter any issues with submodules, you can update them manually:

```bash
git submodule update --init --recursive
```

## 4. Qwen.cpp Compilation

For Qwen.cpp:

```bash
git clone --recursive https://github.com/QwenLM/qwen.cpp.git
cd qwen.cpp
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

## 5. llama.cpp Compilation

For llama.cpp:

```bash
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

## 6. Optimizing Compilation for Kunpeng 920

To optimize for the Kunpeng 920's ARM architecture, you can add specific flags to the CMake command:

```bash
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_FLAGS="-march=armv8.2-a+fp16" -DCMAKE_CXX_FLAGS="-march=armv8.2-a+fp16" ..
```

This enables ARM v8.2 features and FP16 support, which can significantly improve performance on the Kunpeng 920.

You can also enable specific optimizations in the CMake configuration. For example, for llama.cpp:

```bash
cmake -DLLAMA_BLAS=ON -DLLAMA_BLAS_VENDOR=OpenBLAS -DCMAKE_C_FLAGS="-march=armv8.2-a+fp16" -DCMAKE_CXX_FLAGS="-march=armv8.2-a+fp16" ..
```

This enables BLAS support using OpenBLAS, which can accelerate matrix operations.

## 7. Troubleshooting Common Issues

1. **CMake version issues**: If you encounter CMake version issues, make sure you've installed the latest version as described in the prerequisites.

2. **Missing dependencies**: If you encounter missing dependencies, you may need to install additional libraries. For example:

   ```bash
   sudo apt-get install libopenblas-dev
   ```

3. **Compilation errors**: If you face compilation errors, try cleaning the build directory and recompiling:

   ```bash
   rm -rf build
   mkdir build && cd build
   cmake ..
   cmake --build . --config Release
   ```

4. **Performance issues**: If the compiled engine isn't performing as expected, try different optimization flags or consider using profiling tools to identify bottlenecks.

Remember to run `source ~/.bashrc` after modifying your PATH or environment variables.

After successful compilation, you can find the executable in the `build` directory. You can run it to start inferencing with your converted and quantized models.

Note: Always refer to the official documentation and README files of these projects for the most up-to-date compilation instructions, as they may change over time.
