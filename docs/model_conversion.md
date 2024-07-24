# Installing Necessary Dependencies and Tools for LLM Deployment on Huawei Kunpeng 920

This document outlines the process of installing essential dependencies and tools required for deploying large language models (LLMs) on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [Python and Pip](#1-python-and-pip)
2. [PyTorch and Related Libraries](#2-pytorch-and-related-libraries)
3. [Transformers and HuggingFace Libraries](#3-transformers-and-huggingface-libraries)
4. [CUDA and GPU Libraries (if applicable)](#4-cuda-and-gpu-libraries-if-applicable)
5. [Additional Machine Learning Libraries](#5-additional-machine-learning-libraries)
6. [Development and Compilation Tools](#6-development-and-compilation-tools)
7. [Networking and Server Tools](#7-networking-and-server-tools)

## 1. Python and Pip

Ensure you have the latest version of pip installed in your Conda environment:

```bash
conda activate llm  # Activate your Conda environment
pip install --upgrade pip
python -m pip install --upgrade pip
```

## 2. PyTorch and Related Libraries

Install PyTorch and related libraries. Note that the specific version might depend on your CUDA version if you're using GPU acceleration:

```bash
# For CPU-only version
conda install pytorch torchvision torchaudio cpuonly -c pytorch

# If you need a specific version, you can specify it:
pip install torch==2.0.0 torchvision==0.15.0 torchaudio==2.0.0

# Install related libraries
pip install einops
```

## 3. Transformers and HuggingFace Libraries

Install the Transformers library and related HuggingFace tools:

```bash
pip install transformers==4.33.3
pip install accelerate
pip install sentencepiece
pip install transformers_stream_generator
pip install peft
pip install datasets
pip install evaluate
pip install huggingface_hub
```

## 4. CUDA and GPU Libraries (if applicable)

If your Kunpeng 920 setup includes NVIDIA GPUs, you'll need to install CUDA and related libraries. However, the bash history doesn't show CUDA installation, which suggests this might be a CPU-only setup. If you do need GPU support, you would typically install CUDA and cuDNN as per NVIDIA's instructions for your specific GPU model.

## 5. Additional Machine Learning Libraries

Install additional libraries that are often used in ML projects:

```bash
pip install numpy pandas scikit-learn matplotlib
pip install tqdm
pip install tiktoken
pip install bitsandbytes
pip install tabulate
pip install modelscope
pip install xformers
pip install flash_attn
```

## 6. Development and Compilation Tools

Install necessary development and compilation tools:

```bash
# Install GCC and G++ if not already installed
sudo apt-get install gcc g++

# Install CMake if not already installed
# (Refer to the system preparation document for detailed CMake installation)

# Install make
sudo apt-get install make

# Install Ninja build system
sudo apt-get install ninja-build

# Install ccache for faster recompilation
sudo apt-get install ccache
```

## 7. Networking and Server Tools

Install tools for networking, server deployment, and tunneling:

```bash
# Install Gradio for web demos
pip install gradio

# Install FastAPI and Uvicorn for API serving
pip install fastapi uvicorn

# Install Streamlit for interactive web apps
pip install streamlit

# Install ngrok for exposing local servers to the internet
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm64.zip
unzip ngrok-stable-linux-arm64.zip
chmod +x ngrok
./ngrok authtoken YOUR_AUTHTOKEN_HERE

# Install localtunnel as an alternative to ngrok
npm install -g localtunnel

# Install frp for reverse proxy
# (Download the appropriate version for your system from the frp GitHub releases page)
wget https://github.com/fatedier/frp/releases/download/v0.54.0/frp_0.54.0_linux_arm64.tar.gz
tar -zxvf frp_0.54.0_linux_arm64.tar.gz
cd frp_0.54.0_linux_arm64
# Configure and use frpc/frps as needed
```

After installing these dependencies and tools, your system should be well-equipped for deploying and working with large language models. Remember to periodically update these packages, especially if you encounter compatibility issues or need features from newer versions.

Note: Some installations might require `sudo` privileges. Always ensure you trust the source of any software you're installing, especially when using `sudo`.

Also, keep in mind that the versions specified in this document are based on the provided bash history. It's a good practice to check for the latest stable versions of these libraries that are compatible with your specific setup and requirements.
