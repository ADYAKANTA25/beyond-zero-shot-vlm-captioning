# beyond-zero-shot-vlm-captioning
Code, experiments, and supplementary materials for the paper  "Beyond Zero-Shot: Diversifying Caption Generation in Vision-Language Models via In-Context Learning".

# Beyond Zero-Shot: Diversifying Caption Generation in VLMs via In-Context Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Framework: PyTorch](https://img.shields.io/badge/Framework-PyTorch-red.svg)](https://pytorch.org/)

## 📄 Abstract
Large Vision-Language Models (VLMs) have shown impressive zero-shot capabilities in image captioning; however, the adaptation of these general-purpose models to specific tasks remains a critical challenge. While much of the existing research has focused on **Parameter-Efficient Fine-Tuning (PEFT)** and **In-Context Learning (ICL)** in isolation, the interaction between these strategies when applied concurrently is not well understood.

In this paper, we present a systematic analysis of their combined effects across three representative VLM architectures: **Qwen3-VL**, **Llama 3.2-VL**, and **Qwen2-VL**. Our proposed hybrid framework incorporates QLoRA-based fine-tuning and dynamic few-shot prompting, evaluated on the Flickr30k benchmark.

**Key Findings:**
* **Architecture-Dependent Behavior:** Llama 3.2-VL achieves peak performance in zero-shot settings (CIDEr = 1.152) but suffers from *Contextual Interference* when prompted. Conversely, Qwen3-VL acts as a strong meta-learner, where fine-tuning and few-shot prompting complement each other (CIDEr = 1.098).
* **Accuracy-Diversity Trade-off:** Fine-tuning improves semantic alignment with ground-truth captions but consistently reduces the lexical diversity of generated outputs across all architectures.

## 📂 Repository Structure
This repository is organized to facilitate both code replication and manuscript compilation.

```text
beyond-zero-shot-vlm-captioning/
│
├── main.tex                 # Primary LaTeX source for the manuscript
├── references.bib           # Bibliography file
├── doublecol-new.cls        # Journal class file (Required for compilation)
│
├── Fig/                     # High-resolution figures used in the paper
│   ├── architecture.png
│   ├── Combined_Radar_Plots.png
│   └── ... (Other visualization assets)
│
├── Supplementary/           # Supplementary PDF and additional analyses
│
├── requirements.txt         # Python dependencies
├── README.md                # Project documentation
└── .gitignore               # Ignored compilation files
