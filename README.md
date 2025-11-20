# Legal Domain Fine-tuning for Qwen2.5-7B-Instruct

This project demonstrates the complete pipeline for fine-tuning the Qwen2.5-7B-Instruct model on legal domain data using the DISC-Law-SFT dataset and evaluating its performance on the DISC-Law-Eval Benchmark.

## Project Overview

The goal of this project is to adapt a general-purpose language model (Qwen2.5-7B-Instruct) for legal question answering tasks through supervised fine-tuning. The process involves data preparation, model training, and comprehensive evaluation across multiple legal examination datasets.

## Implementation Steps

### 1. Data Preparation
- **Download Training Data**: Obtain the `DISC-LAW-SFT` dataset from [ShengbinYue/DISC-Law-SFT](https://huggingface.co/datasets/ShengbinYue/DISC-Law-SFT) (contains 4 JSONL files)
- **Preprocess Data**: Run `data_precessing.py` to convert the data into LLaMA-Factory compatible format and register it in the LLaMA-Factory dataset registry

### 2. Model & Framework Setup
- **Download Base Model**: Acquire `Qwen2.5-7B-Instruct` from Hugging Face
- **Setup Training Framework**: Clone and setup `LLaMA-Factory` from GitHub

### 3. Model Training
- **Launch Web Interface**: Execute `llamafactory-cli webui` to access the training interface
- **Configure Training**: 
  - Select `Qwen2.5-7B-Instruct` as the base model
  - Choose your preprocessed SFT dataset
  - Set appropriate training parameters (learning rate, epochs, LoRA configuration, etc.)
- **Start Fine-tuning**: Initiate the training process through the web interface

### 4. Evaluation
- **Download Test Data**: Get the evaluation dataset from [DISC-LawLLM Objective Evaluation](https://github.com/FudanDISC/DISC-LawLLM/tree/main/eval/datasets/objective)
- **Generate Predictions**:
  - Run `batch_infer.py` to obtain baseline predictions (pre-trained model) (Reminder: change the address of files)
  - Run `batch_infer.py` again to get fine-tuned model predictions
- **Evaluate Performance**: Execute `eval.py` to calculate and compare performance metrics for both models

## Quick Start

For immediate use, the fine-tuned model is available on Hugging Face:

```python
from transformers import AutoModel, AutoTokenizer

model = AutoModel.from_pretrained("zzy12222/Qwen2.5-7B-Instruct-law")
tokenizer = AutoTokenizer.from_pretrained("zzy12222/Qwen2.5-7B-Instruct-law")