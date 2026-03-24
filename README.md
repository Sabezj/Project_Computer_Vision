# Token Pooling in Vision Transformers — Small-Scale Reproduction

This repository contains a compact reproduction of the main idea from **Token Pooling in Vision Transformers** using a lightweight setup on **CIFAR-10**.

The goal of the project is to compare a baseline Vision Transformer with a pooled version that reduces the number of tokens during processing. The main question is whether token reduction can decrease computational cost while preserving most of the classification quality.

## Project overview

Two models are compared:

- **Baseline ViT** — a compact Vision Transformer without token reduction
- **Pooled ViT** — the same backbone with a token pooling module inserted into the transformer pipeline

The pooled model is designed to reduce:
- sequence length
- attention cost
- memory usage
- training / inference time

while keeping classification accuracy reasonably close to the baseline.

## Repository structure

```text
src/
  token_pooling_project.ipynb

outputs/
  comparison.png
  training_curves.png
  token_counts.png
  pooling_assignment_example.png
  confusion_vit_tiny_baseline.png
  confusion_vit_tiny_token_pool.png
  summary.csv

README.md
report.md
