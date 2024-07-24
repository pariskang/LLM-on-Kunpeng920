# Running Inference and Demos for LLMs on Huawei Kunpeng 920

This document provides detailed instructions on how to run inference and create demos using the compiled large language models (LLMs) on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [Running CLI Demos](#3-running-cli-demos)
   - [ChatGLM](#chatglm)
   - [Baichuan](#baichuan)
   - [Qwen](#qwen)
4. [Running Web Demos](#4-running-web-demos)
5. [Performance Monitoring](#5-performance-monitoring)
6. [Troubleshooting](#6-troubleshooting)

## 1. Introduction

After compiling the inference engines and converting your models, the next step is to run inference and create demos. This allows you to interact with the model, test its capabilities, and showcase its performance on the Huawei Kunpeng 920 platform.

## 2. Prerequisites

Ensure you have:
- Compiled inference engines (ChatGLM.cpp, Qwen.cpp, etc.)
- Converted and quantized model files
- Python 3.8+ with necessary libraries installed

Install required Python libraries:

```bash
pip install gradio transformers torch
```

## 3. Running CLI Demos

### ChatGLM

To run the ChatGLM model in interactive mode:

```bash
cd chatglm.cpp
./build/bin/main -m chatglm-ggml.bin -i
```

For a single prompt:

```bash
./build/bin/main -m chatglm-ggml.bin -p "Hello, how are you?"
```

### Baichuan

To run the Baichuan model:

```bash
cd chatglm.cpp
./build/bin/main -m baichuan13btcm0-ggml.bin -i
```

You can adjust parameters like temperature and top_p:

```bash
python3 examples/cli_demo.py -m baichuan13btcm0-ggml.bin -p "你好" --temp 0.8 --top_p 0.8
```

### Qwen

For Qwen models:

```bash
cd qwen.cpp
./build/bin/main -m qwen1b-ggml.bin --tiktoken "/path/to/qwen/tokenizer/qwen.tiktoken" -i
```

## 4. Running Web Demos

You can create web demos using Gradio. Here's an example for ChatGLM:

```bash
cd chatglm.cpp/examples
python3 web_demo.py -m ../chatglm-ggml.bin
```

For Baichuan:

```bash
python3 web_demo.py -m ../baichuan13btcm0-ggml.bin
```

These commands will start a local web server. You can access the demo through your web browser.

To make your demo accessible from the internet, you can use tools like ngrok:

```bash
ngrok http 7860
```

Replace 7860 with the port number your Gradio app is running on.

## 5. Performance Monitoring

While running inference, it's crucial to monitor system performance:

```bash
# Monitor CPU usage
top

# Monitor memory usage
free -h

# Monitor disk I/O
iostat -x 1
```

For more detailed profiling, you can use tools like `perf`:

```bash
perf record -g ./build/bin/main -m model-ggml.bin -p "Your prompt here"
perf report
```

## 6. Troubleshooting

1. **Out of memory errors**: If you encounter out of memory errors, try using a more aggressive quantization method or reduce the context size if your model supports it.

2. **Slow inference**: Ensure you're using optimized builds (`Release` mode). Also, check if all CPU cores are being utilized.

3. **Incorrect outputs**: Verify that you're using the correct model file and that the conversion process completed successfully. Compare outputs with the original non-quantized model.

4. **Gradio interface not loading**: Ensure all required Python packages are installed and up to date. Check your firewall settings if accessing remotely.

5. **Tokenizer errors**: For models like Qwen, ensure you're providing the correct path to the tokenizer file.

Remember to always refer to the most recent documentation of the respective model repositories, as procedures may change with new updates.

By following these instructions, you should be able to successfully run inference and create demos for your LLMs on the Huawei Kunpeng 920 platform. This will allow you to interact with the models, evaluate their performance, and showcase their capabilities.
