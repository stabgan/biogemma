# BioGemma

Fine-tuned Gemma-3 1B for clinical and biomedical NLP.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Base Model](https://img.shields.io/badge/base-Gemma%203%201B-blue.svg)](https://ai.google.dev/gemma)

---

## Overview

BioGemma is a domain-adapted version of Google's [Gemma 3 1B](https://ai.google.dev/gemma) language model, fine-tuned on biomedical and clinical text for downstream medical NLP tasks such as:

- Medical question answering
- Clinical text comprehension and summarization
- Biomedical entity recognition (drugs, conditions, procedures)
- Medical literature summarization

## Fine-Tuning Approach

| Detail | Value |
|---|---|
| Base model | Google Gemma 3 1B |
| Method | LoRA / QLoRA (parameter-efficient fine-tuning) |
| Training data | Curated medical corpus — PubMed abstracts, medical textbooks, clinical guidelines |
| Hardware | Single-GPU training |

## Dependencies

```
torch
transformers
accelerate
```

Install with:

```bash
pip install torch transformers accelerate
```

## Usage

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

## Known Issues

- **No model weights published yet.** The HuggingFace Hub model (`stabgan/biogemma`) is not available as of this writing. The usage example above will fail until weights are uploaded.
- **No training or evaluation code in this repository.** The repo currently contains only documentation (README + LICENSE). There are no scripts, notebooks, configs, or reproducible training pipelines.
- **No benchmark results.** No evaluation against standard medical NLP benchmarks (MedQA, PubMedQA, MedMCQA) has been published.
- **No requirements file.** Dependencies are inferred from the usage example; there is no `requirements.txt` or `pyproject.toml`.

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
