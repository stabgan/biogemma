# 🧬 BioGemma — Medical LLM based on Google Gemma 3

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Model](https://img.shields.io/badge/base-Gemma%203%201B-blue.svg)](https://ai.google.dev/gemma)
[![HuggingFace](https://img.shields.io/badge/🤗-Model%20Card-orange.svg)](#)

A fine-tuned version of Google's Gemma 3 1B model on medical and biomedical text corpora, optimized for clinical NLP tasks.

## What is BioGemma?

BioGemma adapts the Gemma 3 1B parameter model for the medical domain through fine-tuning on curated biomedical literature, clinical notes patterns, and medical Q&A datasets. The goal is a lightweight, deployable medical language model that can run on a single GPU.

## Use Cases

- **Medical question answering** — Answer clinical and biomedical questions
- **Clinical text understanding** — Parse and interpret medical documentation
- **Medical entity recognition** — Identify drugs, conditions, procedures in text
- **Literature summarization** — Summarize medical research papers and abstracts

## Quick Start

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_name = "stabgan/biogemma"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

prompt = "What are the common symptoms of acute kidney injury?"
inputs = tokenizer(prompt, return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=256)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

## Training Details

- **Base model:** Google Gemma 3 1B
- **Fine-tuning method:** LoRA / QLoRA
- **Training data:** Curated medical corpus (PubMed abstracts, medical textbooks, clinical guidelines)
- **Hardware:** Single GPU training

## Roadmap

- [ ] Publish model weights to HuggingFace Hub
- [ ] Benchmark against MedQA, PubMedQA, MedMCQA
- [ ] Add clinical note generation capabilities
- [ ] RLHF alignment for medical safety
- [ ] Comparison with BioMistral, MedAlpaca, PMC-LLaMA

## Disclaimer

This model is for research purposes only. It is not intended for clinical decision-making or medical diagnosis. Always consult qualified healthcare professionals for medical advice.

## License

MIT License — see [LICENSE](LICENSE) for details.
