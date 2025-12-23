# Beyond Zero-Shot: Diversifying Caption Generation in Vision-Language Models via In-Context Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Framework: PyTorch](https://img.shields.io/badge/Framework-PyTorch-red.svg)](https://pytorch.org/)
[![Research](https://img.shields.io/badge/Type-Academic%20Research-green.svg)]()

This repository contains the **code, experimental setup, figures, and supplementary materials** for the research paper:

> **Beyond Zero-Shot: Diversifying Caption Generation in VLMs via In-Context Learning with Dynamic Example Selection**

The project focuses on understanding how **Parameter-Efficient Fine-Tuning (PEFT)** and **In-Context Learning (ICL)** interact when applied jointly to large Vision-Language Models (VLMs) for image captioning.

---

## 📄 Abstract

Large Vision-Language Models (VLMs) have shown impressive zero-shot capabilities in image captioning; however, adapting these general-purpose models to specific tasks remains a critical challenge. While existing studies often investigate **Parameter-Efficient Fine-Tuning (PEFT)** and **In-Context Learning (ICL)** independently, their combined behavior is not well understood.

This work presents a **systematic empirical study** of the interaction between fine-tuning and few-shot prompting across three representative VLM architectures: **Qwen2-VL**, **Qwen3-VL**, and **Llama 3.2-VL**. We introduce a hybrid adaptation framework that integrates **QLoRA-based fine-tuning** with **dynamic few-shot prompting**, evaluated on the **Flickr30k** benchmark.

Using both lexical and semantic evaluation metrics (BLEU, CIDEr, RefCLIPScore), we observe **architecture-dependent behaviors**, including contextual interference in Llama 3.2-VL and strong meta-learning effects in Qwen3-VL. Additionally, we identify a consistent **accuracy–diversity trade-off**, where fine-tuning improves semantic alignment but reduces lexical diversity. These findings provide practical guidance for selecting adaptation strategies when deploying VLMs in real-world captioning systems.

---

## 🎯 Key Contributions

- Systematic analysis of **fine-tuning and in-context learning interaction** in VLMs
- Empirical evidence of **contextual interference** in fine-tuned Llama-based models
- Identification of **meta-learning behavior** in Qwen3-VL
- Quantitative study of the **accuracy–diversity trade-off**
- Lightweight, reproducible adaptation using **QLoRA**

---

## 🧠 Models Evaluated

| Model        | Parameters | Adaptation Settings |
|--------------|------------|---------------------|
| Qwen2-VL     | 7B         | Base / Fine-Tuned / Few-Shot |
| Qwen3-VL     | 8B         | Base / Fine-Tuned / Few-Shot |
| Llama 3.2-VL | 11B        | Base / Fine-Tuned / Few-Shot |

All models are evaluated under:
- Zero-shot inference
- Few-shot inference (K = 3)
- Consistent nucleus sampling strategy

---

## 📊 Dataset

### Flickr30k
- 31,783 images
- 5 human-written captions per image
- Standard benchmark for image captioning

To ensure fair evaluation:
- **Support set:** 21,000 images (used for fine-tuning and in-context examples)
- **Test set:** 100 held-out images (never used during training)

---

## 📂 Repository Structure

```
beyond-zero-shot-vlm-captioning/
│
├── README.md                  # Main documentation (high-level)
├── requirements.txt           # Python dependencies (for reproducibility)
├── .gitignore                 # Ignore LaTeX build files, cache, etc.
│
├── paper/
│   ├── main.tex               # Main LaTeX manuscript
│   ├── references.bib         # Bibliography
│   ├── doublecol-new.cls      # Journal class file
│
├── figures/
│   ├── architecture.png
│   ├── Combined_Radar_Plots.png
│   ├── bleu_comparison.png
│   ├── cider_comparison.png
│   └── ...                    # All figures used in paper
│
├── supplementary/
│   ├── Supplementary.pdf      # Final supplementary material
│   ├── Fig_S1.png
│   ├── Fig_S2.png
│   ├── ...
│   └── Fig_S10.png
│
├── experiments/
│   ├── configs/
│   │   ├── qlora_qwen2.yaml
│   │   ├── qlora_qwen3.yaml
│   │   └── qlora_llama32.yaml
│   │
│   ├── prompting/
│   │   ├── zero_shot.txt
│   │   └── few_shot_template.txt
│   │
│   └── evaluation_protocol.md
│
└── LICENSE


```


⚙️ Installation & Environment Setup

This project uses Python 3.10 and PyTorch.

Environment Setup:


python -m venv vlm_env

source vlm_env/bin/activate

pip install -r requirements.txt

Hardware Notes

Experiments were conducted on NVIDIA GPUs with at least 40GB VRAM (A100 class).
All results reported in the paper were obtained using a single GPU with QLoRA-based fine-tuning.


✔ Simple  
✔ Reproducible  
✔ No over-engineering  


---

🔧 Fine-Tuning Strategy

We employ QLoRA-based Parameter-Efficient Fine-Tuning to adapt VLMs without updating full model weights.

Key characteristics:



4-bit NF4 quantization
Low-rank adapters applied to attention and MLP layers
Single-epoch fine-tuning
No full-parameter updates

Model-specific configurations are provided in:
 experiments/configs/


---

🧩 In-Context Learning & Prompting

Models are evaluated under both zero-shot and few-shot prompting.

Few-Shot Prompting

Number of in-context examples: K = 3

Examples sampled from the Flickr30k support set

Identical nucleus sampling strategy used across all experiments

Prompt templates are available in:
 experiments/prompting/

Dynamic example selection is used to reduce prompt bias and contextual redundancy.


---

📏 Evaluation Protocol

Caption quality is evaluated using lexical, semantic, and visual grounding metrics:

BLEU-1 / BLEU-4

ROUGE-L

METEOR

CIDEr

BERTScore

CLIPScore

RefCLIPScore

Distinct-1 / Distinct-2

All metrics are computed on the held-out test set.

Detailed evaluation procedures are documented in:
experiments/evaluation_protocol.md


---

♻️ Reproducibility

Fixed random seeds across runs

Identical decoding parameters for all models

No test images used during fine-tuning or prompt construction

Configuration files and prompt templates are fully released

Due to licensing and storage constraints, datasets and model checkpoints are not redistributed.


---

📚 Citation



@article{beyond_zeroshot_vlm,
  title     = {Beyond Zero-Shot: Diversifying Caption Generation in Vision-Language Models via In-Context Learning},
  author    = {Sahoo, Adyakanta},
  journal   = {Under Review},
  year      = {2025}
}

---


📜 License
This project is released under the MIT License.
See the LICENSE file for details.

---

⚠️ Disclaimer

This repository is intended for academic and research purposes only.
The reported results reflect controlled experimental settings and may not directly generalize to all deployment scenarios.

