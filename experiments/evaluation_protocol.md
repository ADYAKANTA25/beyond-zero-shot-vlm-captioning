# Evaluation Protocol

This document describes the evaluation procedure used for all experiments
reported in the paper *Beyond Zero-Shot: Diversifying Caption Generation in Vision-Language Models via In-Context Learning*.

The protocol is designed to ensure fairness, reproducibility, and consistency
across models, prompting strategies, and adaptation settings.

---

## Inference Settings

All models were evaluated using stochastic decoding to reflect realistic
caption generation behavior.

- Decoding strategy: Nucleus Sampling
- Temperature (T): 0.8
- Top-p: 0.9
- Top-k: 50
- Maximum generation length: 128 tokens
- Number of generated captions per image: 5

The same decoding configuration was applied to:
- Zero-shot inference
- Few-shot inference (K = 3)
- Base and fine-tuned models

This ensures that performance differences arise from adaptation strategies
rather than sampling variations.

---

## Prompting Conditions

### Zero-Shot
Models receive a single instruction prompt requesting a descriptive image caption,
without any in-context examples.

### Few-Shot
Each query image is preceded by K = 3 dynamically sampled image-caption pairs
from the support set. These examples are randomly selected per query to avoid
memorization or fixed prompt bias.

---

## Dataset Splits

- Support Set: 21,000 images from Flickr30k
  - Used for QLoRA fine-tuning
  - Used as the pool for in-context examples

- Query/Test Set: 100 held-out images
  - Never used during training
  - Never included in the support set
  - Used exclusively for evaluation

This strict separation prevents information leakage.

---

## Evaluation Metrics

### Lexical Accuracy
- BLEU-1 to BLEU-4
- ROUGE-L
- METEOR

These metrics evaluate n-gram overlap and sentence-level structure.

---

### Semantic Relevance
- CIDEr
- BERTScore

CIDEr measures consensus with human-written captions using TF-IDF weighting.
BERTScore measures contextual semantic similarity using pretrained embeddings.

---

### Visual-Semantic Alignment
- CLIPScore
- RefCLIPScore

These metrics assess alignment between generated captions and visual content
in a shared embedding space.

---

### Generative Diversity
- Distinct-1
- Distinct-2

These metrics measure lexical diversity across generated captions and are used
to analyze the accuracy–diversity trade-off.

---

## Statistical Analysis

- All reported scores are averaged across the test set
- Statistical significance is assessed using paired comparisons
- Results are interpreted in terms of relative trends rather than absolute values

---

## Reproducibility Notes

- All experiments were conducted using the same random seed per configuration
- Model weights, prompts, and decoding parameters were held constant across comparisons
- Differences in results are attributed solely to adaptation strategy and architecture
