# Beyond Scaling: Bayesian Temporal Inductive Bias for Time-Series Foundation Model Adaptation

**Authors:** Yunbo Mei, Leheng Zhou, Yunli Su, and Xinjie Lan

**Venue:** Accepted as a regular paper at the Workshop on Large Models for Time Series Data Mining (LM4TED), IEEE ICDM 2026.

## Overview

Time-series foundation models (TSFMs) learn transferable representations through large-scale pretraining, but increasing model capacity does not consistently improve forecasting accuracy. Temporal dependencies can also vary across input windows and regimes, motivating adaptation of the model's temporal inductive bias.

This work develops a Bayesian interpretation of attention that connects a content-based prior with positional temporal weighting. Motivated by the limitations of static lag-based positional biases, we propose an adaptive mixture of temporal kernels for pretrained Transformer-based TSFMs. The method is designed for incorporation into standard multi-head self-attention; the experiments in this paper evaluate its instantiation in Timer-XL.

## Method

- **Temporal experts:** A bank of RBF and periodic kernels represents local, periodic, and long-range dependency patterns.
- **Temporal evidence:** Content-based attention logits are aggregated by relative lag to form a temporal-evidence profile, which is concatenated with its Fourier magnitude spectrum.
- **Adaptive routing:** An MoE router produces input- and head-specific mixture weights, with top-k selection and renormalization.
- **Adaptive positional bias:** The logarithm of the resulting temporal kernel mixture is added to the attention logits before softmax. The router and backbone are jointly fine-tuned on the target dataset while the candidate kernels and their hyperparameters remain fixed.

## Evaluation

Experiments on ETTh1, ETTh2, ETTm1, ETTm2, and Weather show average MSE and MAE reductions of 3.4% and 3.0% over zero-shot Timer-XL, and 2.1% and 2.0% over full-shot Timer-XL, respectively, with a 7.2% increase in parameter count. These are average improvements across the evaluated settings.

## Repository Status

This repository currently provides an overview of the paper. Implementation code is not yet available.
