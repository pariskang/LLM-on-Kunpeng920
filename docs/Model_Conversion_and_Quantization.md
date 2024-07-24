# Model Conversion and Quantization for LLM Deployment on Huawei Kunpeng 920

This document provides detailed instructions on how to convert and quantize large language models (LLMs) for efficient deployment on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [ChatGLM Model Conversion](#3-chatglm-model-conversion)
4. [Baichuan Model Conversion](#4-baichuan-model-conversion)
5. [Qwen Model Conversion](#5-qwen-model-conversion)
6. [GGML Format Conversion](#6-ggml-format-conversion)
7. [Quantization Techniques](#7-quantization-techniques)
8. [Verifying Converted Models](#8-verifying-converted-models)

## 1. Introduction

Model conversion and quantization are crucial steps in deploying large language models on hardware with limited resources. These processes help reduce model size and improve inference speed while maintaining acceptable performance.

## 2. Prerequisites

Before proceeding, ensure you have:

- Python 3.8+ installed
- Required libraries: transformers, torch, sentencepiece, accelerate
- Sufficient disk space for model weights
- Access to the original model weights (usually downloaded from Hugging Face or other model hubs)

```bash
pip install transformers torch sentencepiece accelerate
```

## 3. ChatGLM Model Conversion

To convert ChatGLM models, use the following steps:

```bash
cd chatglm.cpp
python3 chatglm_cpp/convert.py -i /path/to/chatglm/model -t q4_0 -o chatglm-ggml.bin
```

Replace `/path/to/chatglm/model` with the actual path to your ChatGLM model.

The `-t q4_0` flag specifies the quantization type. You can choose different quantization types based on your needs:

- `q4_0`: 4-bit quantization (smallest size, fastest inference, some quality loss)
- `q4_1`: 4-bit quantization with different algorithm
- `q5_0`: 5-bit quantization
- `q8_0`: 8-bit quantization (larger size, slower inference, better quality)

## 4. Baichuan Model Conversion

For Baichuan models, use a similar process:

```bash
python3 chatglm_cpp/convert.py -i /path/to/baichuan/model -t q4_0 -o baichuan-ggml.bin
```

If you're converting a fine-tuned Baichuan model, you can specify the path to the fine-tuned weights:

```bash
python3 chatglm_cpp/convert.py -i /path/to/baichuan/model -t q4_0 -o baichuan-finetuned-ggml.bin -l /path/to/finetuned/weights
```

## 5. Qwen Model Conversion

For Qwen models, the process is slightly different:

```bash
cd qwen.cpp
python3 qwen_cpp/convert.py -i /path/to/qwen/model -t q4_0 -o qwen-ggml.bin
```

Note that Qwen models may require a specific tokenizer file:

```bash
./build/bin/main -m qwen-ggml.bin --tiktoken "/path/to/qwen/tokenizer/qwen.tiktoken" -i
```

## 6. GGML Format Conversion

The GGML format is commonly used for efficient inference on CPU. The conversion scripts provided above typically handle the conversion to GGML format automatically.

## 7. Quantization Techniques

Quantization reduces model precision to decrease size and increase inference speed. Common quantization types include:

- INT8: 8-bit integer quantization
- INT4: 4-bit integer quantization
- Mixed precision: Combination of different quantization levels for different parts of the model

The `-t` flag in the conversion scripts specifies the quantization type. Experiment with different types to find the best balance between model size, inference speed, and output quality for your use case.

## 8. Verifying Converted Models

After conversion, it's crucial to verify the model's performance:

```bash
# For ChatGLM and Baichuan models
./build/bin/main -m model-ggml.bin -i

# For Qwen models
./build/bin/main -m qwen-ggml.bin --tiktoken "/path/to/qwen/tokenizer/qwen.tiktoken" -i
```

This will start an interactive session where you can test the model's outputs.

Remember to compare the outputs of the quantized model with the original model to ensure acceptable quality. You may need to adjust the quantization parameters if you observe significant degradation in performance.

Note: The exact paths and filenames may vary depending on your specific setup and the versions of the models you're using. Always refer to the most recent documentation of the respective model repositories for the most up-to-date instructions.
