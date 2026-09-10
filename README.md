# Hehebbian-Riddiculum
# Hehebbian Riddiculum: Switching Between Learning Rules

> **Neuromatch Academy (NMA) Group Project**

## Overview

**Hehebbian Riddiculum** investigates whether combining or switching between multiple learning rules can enable more efficient and biologically plausible learning than using a single learning rule throughout training.

The project explores this question in both **rate-based recurrent neural networks (RNNs)** and **spiking neural networks (SNNs)**. We study a controller-based framework in which network activity is used to gate different learning rules, allowing different plasticity mechanisms to be selected during learning.

## Research Question

> **Can combining or switching between multiple learning rules produce more efficient, biologically plausible learning, rather than using a single rule?**

The motivation is based on the observation that biological brains may employ multiple plasticity mechanisms operating together and across different timescales, in contrast to artificial neural networks that often rely on a single optimization rule throughout training.

## Approach

The project investigates switching between different learning rules using a controller-based mechanism.

The explored learning mechanisms include:

* Hebbian learning / STDP
* Contrastive Hebbian Learning (CHL)
* Backpropagation (BP)
* Oja-style learning
* E-prop

A controller receives information from the network and uses this information to gate learning rules.

The framework was based on the switching synaptic plasticity approach described by **Turcu et al. (2026)**.

## Datasets and Tasks

For the experiments, we considered temporal and neuromorphic variants of MNIST, including:

* **Sequential MNIST (sMNIST)**
* **Neuromorphic MNIST (N-MNIST)**

For the RNN experiments, different augmentation conditions were used to examine how different learning rules performed under different types of transformations and information degradation.

## Experiments

### RNNs

We investigated whether neurons could gradually select the locally more suitable learning rule through biologically inspired competition between neighboring neurons.

The experiments compared conditions in which neurons selected between different learning rules, including **CHL** and **backpropagation**.

The tested augmentation conditions included:

* Normal augmentation
* Affine augmentation
* Elastic augmentation
* Perspective augmentation
* Blur augmentation
* Random Erasing augmentation
* Random Transform augmentation
* Mixed augmentation

### SNNs

The same general controller framework was also evaluated in spiking neural networks using **N-MNIST**.

We compared:

* Activity-based switching
* Probabilistic/random switching
* Frozen learning-rule conditions
* All-credit E-prop

The experiments also examined practical training issues related to recurrent weight initialization and weight growth.

## Key Findings

### RNNs

The experiments suggested complementary strengths between the learning rules.

**Backpropagation (BP)** consistently performed better on tasks involving structured geometric transformations, while **CHL** performed better under information loss and noisy conditions.

These results suggest that different learning rules may have different inductive biases and may therefore contribute differently depending on the learning environment.

### SNNs

For the N-MNIST experiments:

* Activity-based switching consistently outperformed probabilistic/random switching.
* However, activity-based switching did not outperform the frozen or all-credit E-prop baselines.
* Oja's decay term was insufficient to prevent exploding weights, which was addressed with an explicit row-norm cap.
* An initially all-excitatory recurrent-weight initialization led to saturated firing and was addressed using signed-random initialization.

## Conclusion

The experiments indicate that switching between learning rules can be useful when the task provides opportunities for different learning mechanisms to contribute complementary advantages.

However, the results also suggest that task design is critical. When the task does not sufficiently favor different learning rules under different conditions, **BPTT remains the strongest update rule** in the experiments considered.

For SNNs, **Oja pre-training followed by E-prop training** produced slightly higher accuracy than using E-prop throughout training.

## Future Directions

Several directions were identified for further investigation:

* Designing tasks in which different learning rules can make distinct and complementary contributions
* Evaluating the approach on more biologically relevant datasets
* Investigating additional local learning rules
* Investigating the non-convergence observed in the Hebbian meta-learning-rate trial

## Project Materials

This repository currently contains the project presentation documenting the research question, methodology, experiments, findings, and future directions.

The original implementation code from the NMA group project is **not included in this repository**.

## Presentation

The project presentation is available in:

```text
presentation/
└── HehebbianRiddiculum-NMAProject.pdf
```

## Team

* Het Thakkar
* Aayushi Vishnoi
* Mauricio A. Diaz
* Shekhar Nath Prakas
* Bhaskar Roy
* Nalin Dhiman
* Yuxin Feng
* Su Zhang
* Vikramaditya Bisani

## Acknowledgement

This project was completed as a group project during **Neuromatch Academy (NMA)**.

The project was inspired by and based on the framework developed in:

> Turcu et al. (2026), *Learning using switching synaptic plasticity rules*.

## Note on Reproducibility

This repository is intended as a record of the NMA project and its research findings. Because the original project source code is not currently available, the repository does not claim to provide a complete reproduction of the original experiments.
