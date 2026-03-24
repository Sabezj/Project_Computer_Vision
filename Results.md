# Project Results — Token Pooling in Vision Transformers

## Overview

The goal of this project was to compare two compact image classification models:

- **Baseline ViT** — a small Vision Transformer without token reduction
- **Token Pooling ViT** — the same backbone with a token pooling stage that reduces the number of visual tokens during processing

The comparison was performed on **CIFAR-10** in a lightweight experimental setup.

---

## Final quantitative results

### Baseline ViT
- **Best validation accuracy:** 0.6296
- **Test accuracy:** 0.6227
- **Training time:** ~69.2 minutes
- **Sequence length:** 65 tokens
- **Approximate attention cost:** 29.94M
- **Attention memory proxy:** 28.88 MB

### Token Pooling ViT
- **Best validation accuracy:** 0.6110
- **Test accuracy:** 0.6022
- **Training time:** ~46.9 minutes
- **Sequence length after pooling:** 17 tokens
- **Approximate attention cost:** 17.29M
- **Attention memory proxy:** 13.51 MB

---

## Main comparison

The baseline model achieved the best classification accuracy, but it was also more expensive.

The pooled model:
- reduced the token sequence from **65** to **17**
- reduced the attention cost proxy from **29.94M** to **17.29M**
- reduced the attention memory proxy from **28.88 MB** to **13.51 MB**
- trained noticeably faster

At the same time, the accuracy drop was relatively small:
- validation accuracy decreased by about **1.9 percentage points**
- test accuracy decreased by about **2.0 percentage points**

---

## What these results mean

These results confirm the main idea behind token pooling:

### 1. Token reduction really lowers computation
The pooled model processes a much shorter token sequence in later stages of the network. Since transformer attention depends strongly on sequence length, this leads to lower computational cost and lower memory usage.

### 2. Efficiency improves without destroying performance
The pooled model is clearly cheaper, but the drop in classification quality is moderate rather than catastrophic. This is important because it means the removed tokens were not all equally necessary for final prediction.

### 3. The baseline model still preserves more information
The baseline model performs slightly better because it keeps the full token sequence throughout the network. This allows it to preserve more fine-grained visual information.

### 4. The trade-off is meaningful
The project demonstrates a realistic efficiency–accuracy trade-off:

- **Baseline ViT** — better accuracy, higher cost
- **Token Pooling ViT** — lower cost, slightly lower accuracy

This is exactly the type of behavior that makes token pooling useful in practice.

---

## Training behavior

The training curves show that both models learned in a stable way.  
The pooled model followed a trajectory similar to the baseline, but consistently stayed slightly below it in validation accuracy.

This suggests that token pooling does not break optimization. Instead, it introduces an efficiency constraint that slightly reduces representational capacity.

---

## Qualitative interpretation

The token-count visualization shows that the pooled model successfully compresses the sequence.  
The pooling assignment visualization also supports the idea that multiple visual tokens can be merged into a smaller representation.

This means the project does not only show a numerical difference in accuracy, but also demonstrates the actual structural effect of token pooling inside the model.

---

## Final conclusion

The results show that the compact reproduction was successful.

The project demonstrates that:

- reducing the number of visual tokens lowers transformer cost
- a shorter token sequence reduces memory and runtime
- the pooled model remains competitive despite using fewer tokens
- token pooling is a practical way to trade a small amount of accuracy for a noticeable gain in efficiency

This should be interpreted as a **small-scale proof of concept** rather than a full-scale reproduction of the original paper.  
Even in this lightweight setup, the central idea of the method is clearly visible and supported by the results.
