# Paper Overview — Token Pooling in Vision Transformers

## Original paper

**Title:** Token Pooling in Vision Transformers  
**Authors:** Dmitrii Marin, Jen-Hao Rick Chang, Anurag Ranjan, Anish Prabhu, Mohammad Rastegari, Oncel Tuzel

**Original paper links:**
- [OpenReview page](https://openreview.net/forum?id=EGtUVDm991w)
- [arXiv page](https://arxiv.org/abs/2110.03860)

---

## Main idea

The paper studies how to make Vision Transformers more efficient by reducing the number of tokens processed in later layers. Instead of keeping the full token sequence through the entire network, the authors propose **Token Pooling**, a data-aware downsampling strategy that removes redundancy in token representations while preserving most of the useful information.

The main intuition is that after self-attention, token representations become smoother and more redundant. Because of this, some tokens can be merged or approximated without a large loss in quality. This allows the model to reduce computation and memory usage while keeping accuracy relatively close to the original transformer.

---

## Motivation

Vision Transformers are powerful, but their computational cost grows quickly with the sequence length. In image models, smaller patches usually improve representation quality, but they also increase the number of tokens and make attention more expensive.

The paper argues that reducing complexity only inside the attention operation is not always enough, because a large part of the overall computation is also spent in fully connected layers. For this reason, the authors focus on reducing the number of tokens themselves, which decreases the cost of multiple parts of the network.

---

## Method summary

The proposed method introduces a token downsampling step inside the transformer pipeline.

At a high level, the method works as follows:

1. The image is converted into a sequence of patch tokens.
2. Transformer layers process these tokens as usual.
3. A token pooling stage compresses the sequence by grouping similar tokens.
4. The reduced token set is passed to the next transformer layers.
5. The final prediction is made from the shorter sequence.

The paper formulates token reduction as an approximation problem: the goal is to represent the original set of tokens with a smaller set while minimizing reconstruction error. In the full method, this is solved through a clustering-based procedure.

---

## Why this paper is interesting

This paper is interesting because it focuses on a very practical trade-off:

- fewer tokens
- lower computation
- lower memory usage
- slightly reduced accuracy

Instead of changing the whole transformer architecture, the method modifies one important part of the pipeline: how many tokens are preserved after intermediate processing. This makes the idea modular and easy to compare against a baseline Vision Transformer.

---

## Why a small-scale reproduction makes sense

A full reproduction of the paper would require larger datasets and stronger training settings. However, the core idea can still be studied in a compact educational setup:

- build a small baseline Vision Transformer
- add a token pooling stage
- compare token count, runtime, and classification accuracy
- analyze the trade-off between efficiency and quality

This kind of simplified experiment is enough to demonstrate the central claim of the paper: reducing token redundancy can improve efficiency without completely destroying model performance.

---

## What is reproduced in this project

This project focuses on a **small-scale reproduction of the main idea**, not on reproducing the exact training setup of the original paper.

The implemented version keeps the same high-level goal:

- compare a baseline ViT with a token-reduced variant
- study how token reduction changes sequence length and compute
- evaluate whether the pooled model remains competitive on image classification

The project is intended to demonstrate the mechanism and intuition behind token pooling in a lightweight setting.

---

## Takeaway

The key message of the paper is that not all visual tokens are equally necessary at every stage of the network. If redundant tokens are removed in a principled way, a Vision Transformer can become significantly more efficient while preserving most of its predictive power.
