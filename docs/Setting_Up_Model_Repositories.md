# Cloning and Setting Up Model Repositories for LLM Deployment on Huawei Kunpeng 920

This document provides step-by-step instructions for cloning and setting up various model repositories for large language model (LLM) deployment on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [Preliminary Steps](#1-preliminary-steps)
2. [Baichuan Model](#2-baichuan-model)
3. [ChatGLM Model](#3-chatglm-model)
4. [Qwen Model](#4-qwen-model)
5. [LLaMA Model](#5-llama-model)
6. [Additional Repositories](#6-additional-repositories)

## 1. Preliminary Steps

Before cloning repositories, ensure you have Git installed and configured:

```bash
# Install Git if not already installed
sudo apt-get install git

# Configure Git (replace with your information)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Create a directory for your projects
mkdir ~/llm_projects
cd ~/llm_projects
```

## 2. Baichuan Model

Clone and set up the Baichuan model repository:

```bash
# Clone Baichuan repository
git clone https://github.com/baichuan-inc/Baichuan2.git
cd Baichuan2

# Install dependencies
pip install -r requirements.txt

# If you encounter issues with specific packages, you might need to install them separately
pip install modelscope
pip install transformers==4.33.3
pip install accelerate
pip install sentencepiece

# For fine-tuning (if needed)
cd fine-tune
# Ensure you have the necessary data files in the data directory
```

## 3. ChatGLM Model

Clone and set up the ChatGLM model repository:

```bash
# Clone ChatGLM repository
git clone --recursive https://github.com/THUDM/ChatGLM-6B.git
cd ChatGLM-6B

# Install dependencies
pip install -r requirements.txt

# You might need to install additional packages
pip install cpm_kernels
pip install icetk

# For using the cpp version
cd ..
git clone --recursive https://github.com/li-plus/chatglm.cpp.git
cd chatglm.cpp

# Build the project (ensure you have CMake installed)
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

## 4. Qwen Model

Clone and set up the Qwen model repository:

```bash
# Clone Qwen repository
git clone --recursive https://github.com/QwenLM/Qwen.git
cd Qwen

# Install dependencies
pip install -r requirements.txt

# For the cpp version
cd ..
git clone --recursive https://github.com/QwenLM/qwen.cpp.git
cd qwen.cpp

# Build the project
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

## 5. LLaMA Model

Clone and set up the LLaMA model repository:

```bash
# Clone LLaMA repository
git clone https://github.com/facebookresearch/llama.git
cd llama

# Install dependencies
pip install -r requirements.txt

# For the cpp version
cd ..
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp

# Build the project
make
```

## 6. Additional Repositories

Here are some additional repositories that might be useful:

```bash
# Clone LLaMA Factory
git clone https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
pip install -r requirements.txt

# Clone FastChat
git clone https://github.com/lm-sys/FastChat.git
cd FastChat
pip install -e .

# Clone ChatGLM-Tuning
git clone https://github.com/mymusise/ChatGLM-Tuning.git
cd ChatGLM-Tuning
pip install -r requirements.txt
```

After cloning and setting up these repositories, you'll have access to a wide range of models and tools for LLM deployment and fine-tuning. Remember to activate your Conda environment before running these commands, and make sure you have sufficient disk space for these large repositories and models.

Note: The exact versions of the models and the content of the repositories may change over time. Always refer to the official documentation of each project for the most up-to-date information on setup and usage.

Also, be aware that some models may require additional steps for downloading weights or setting up specific configurations. Check the README files in each repository for detailed instructions.
