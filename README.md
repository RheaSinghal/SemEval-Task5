# SemEval-Task5
blue at SemEval-2026 Task 5

## NarrBERT: Narrative-Aware BERT for Graded WSD

This repository contains our submission to **SemEval-2026 Task 5 (AmbiStory)**.
The task requires predicting a **plausibility score (1–5)** for a candidate word sense given a five-sentence narrative.

---

## Approach

We model the task as a **regression problem** using a **BERT cross-encoder**.

### Input Format

```
[CLS] Full Narrative Context [SEP] Sense Definition + Example [SEP]
```

* Backbone: `bert-base-uncased`
* Objective: Mean Squared Error (MSE)
* Output: Continuous score (1–5)

Unlike bi-encoders, the cross-encoder allows direct token-level interaction between story context and sense gloss.

We additionally apply **post-hoc linear calibration** to better align predictions with human rating distributions.

---

## Results

### Development Set

* Sentence-Transformer (Bi-Encoder): **0.52**
* BERT-Base (Initial): **0.58**
* **BERT-Base (Tuned): 0.66**
* BERT-Large: **0.64**

### Official Test Set

* **Spearman:** 0.4866
* **Accuracy-within-SD:** 0.6613 (615/930)

