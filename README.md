# BioGemma

Fine-tuned Gemma 3 1B for clinical and biomedical NLP.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Base Model](https://img.shields.io/badge/base-Gemma%203%201B-blue.svg)](https://ai.google.dev/gemma)
[![HuggingFace](https://img.shields.io/badge/%F0%9F%A4%97-stabgan%2Fbiogemma-orange)](https://huggingface.co/stabgan/biogemma)

---

## Overview

BioGemma is a domain-adapted version of Google's [Gemma 3 1B](https://ai.google.dev/gemma) language model, fine-tuned on biomedical and clinical text. Target tasks include:

- Medical question answering
- Clinical text comprehension and summarization
- Biomedical entity recognition (drugs, conditions, procedures)
- Medical literature summarization

## Fine-Tuning Details

| Detail | Value |
|---|---|
| Base model | Google Gemma 3 1B |
| Method | LoRA / QLoRA (parameter-efficient fine-tuning) |
| Training data | Curated medical corpus — PubMed abstracts, medical textbooks, clinical guidelines |
| Hardware | Single-GPU training |

## 🛠 Tech Stack

| | Technology | Purpose |
|---|---|---|
| 🧠 | [Gemma 3 1B](https://ai.google.dev/gemma) | Base language model |
| 🔥 | [PyTorch](https://pytorch.org/) | Deep learning framework |
| 🤗 | [Transformers](https://huggingface.co/docs/transformers) | Model loading and inference |
| 🚀 | [Accelerate](https://huggingface.co/docs/accelerate) | Multi-device model distribution |
| 🎯 | [PEFT / LoRA](https://huggingface.co/docs/peft) | Parameter-efficient fine-tuning |

## Installation

```bash
pip install torch transformers accelerate
```

## Usage

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM

model_name = "stabgan/biogemma"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    dtype=torch.bfloat16,
    device_map="auto",
)

prompt = "What are the common symptoms of acute kidney injury?"
inputs = tokenizer(prompt, return_tensors="pt").to(model.device)
outputs = model.generate(**inputs, max_new_tokens=256)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

## ⚠️ Known Issues

- **No model weights published yet.** The HuggingFace Hub model (`stabgan/biogemma`) is not available as of this writing. The usage example above will fail until weights are uploaded.
- **No training or evaluation code in this repository.** The repo currently contains only documentation. There are no scripts, notebooks, configs, or reproducible training pipelines.
- **No benchmark results.** No evaluation against standard medical NLP benchmarks (MedQA, PubMedQA, MedMCQA) has been published.

## Roadmap

- [ ] Publish model weights to HuggingFace Hub
- [ ] Add training and evaluation scripts
- [ ] Benchmark against MedQA, PubMedQA, MedMCQA
- [ ] Clinical note generation capabilities
- [ ] RLHF alignment for medical safety

## Disclaimer

This model is for **research purposes only**. It is not intended for clinical decision-making or medical diagnosis. Always consult qualified healthcare professionals for medical advice.

## License

[MIT](LICENSE)
