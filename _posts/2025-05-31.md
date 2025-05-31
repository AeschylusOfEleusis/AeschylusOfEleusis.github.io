---
layout:   post
title: "Machine Learning"
date: 2025-05-31 10:00:00 +0800
categories: [Machine Learning]
tags: [Machine Learning, Probability Information Risk, Numerical Relativity, Quantum Field Theory]
math:       true        # enable KaTeX
---


# Notes on Machine Learning (Draft)

## Abstract

Notes for an annotated bibliography are provided as bare bones.

---
*(Textbooks: Bishop-24 DL, Goodfellow-16 DL, Murphy-22 PML-Intro, Murphy-23 PML-Adv, Bishop-06 PRML.
External references = S1 … S64, each hyper-linked and explained in one unique sentence.)*


## 1 Overview

### Chapters

* **Bishop-24 Ch 1** – Historical tour with modern DL vocabulary.
* **Goodfellow-16 Ch 1** – Frames DL as the third wave of AI.
* **Murphy-22 Ch 1 & Ch 5** – Rational decision-making in uncertain worlds.
* **Murphy-23 Ch 1** – Overview of the landscape.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S1  | [arXiv 1301.7115](https://arxiv.org/abs/1301.7115)                             | Early deep-learning breakthroughs.   |
| S2  | [arXiv 1803.08823](https://arxiv.org/abs/1803.08823)                           | Gives physicists a lay-of-the-land tour of ML. |
| S4  | [arXiv 1903.10563](https://arxiv.org/abs/1903.10563)                           | Surveys DL’s adoption across the physical sciences.         |
| S5  | [Springer book 2020](https://link.springer.com/book/10.1007/978-3-030-40245-7) | Quantum-mechanics problems offer DL research.                     |
| S7  | [Nature Phys 2020](https://www.nature.com/articles/s41567-020-0929-2)          | Snapshot geared toward a physics readership.                            |
| S8  | [arXiv 2104.03902](https://arxiv.org/abs/2104.03902)                           | Speculates on a universe that trains itself.    |
| S9  | [arXiv 2104.00008](https://arxiv.org/abs/2104.00008)                           | AI & physics on a single timeline.                   |
| S11 | [arXiv 2408.00082](https://arxiv.org/abs/2408.00082)                           | TASI lectures as conceptual gateway.                                     |

---

## 2 Probability & Statistical Foundations

### Chapters

* **Bishop-24 Ch 2–3** – Bayes, KL-divergence and catalogue of common distributions.
* **Goodfellow-16 Ch 2–4** – Linear algebra, probability, information.
* **Murphy-22 Ch 2-4 & 6** – Univariate & multivariate probability. Linear algebra.
* **Murphy-23 Ch 2–3 & 5** – Condensed reiteration.
* **PRML-06 App B–C** – Reference tables for distributions and matrix identities.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S22 | [arXiv cond-mat/9607180](https://arxiv.org/abs/cond-mat/9607180) | Re-derives priors from maximum-entropy field theory.   |
| S23 | [arXiv cond-mat/0009165](https://arxiv.org/abs/cond-mat/0009165) | Extends the field-theoretic argument to dynamic data.            |
| S24 | [PubMed 25018724](https://pubmed.ncbi.nlm.nih.gov/25018724/)     | Neuroscience model averaging parameter uncertainty.         |
| S26 | [arXiv 2112.01388](https://arxiv.org/abs/2112.01388)             | Residual-prior pipeline for deep nets with resilience of theoretical priors to engineering.    |
| S27 | [arXiv 2305.10491](https://arxiv.org/abs/2305.10491)             | Renormalisation and Bayesian evidence. |

---

## 3 Linear Regression & Generalised Linear Models

### Chapters

* **Bishop-24 Ch 4** – Single-layer network ordinary least squares.
* **Murphy-22 Ch 8 & 12** – From homoskedastic Gaussian models to Poisson/Bernoulli GLMs.
* **Murphy-23 Ch 15** – Asymptotic statistical treatment of GLM inference.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S12 | [arXiv 1702.01522](https://arxiv.org/abs/1702.01522) | Converts inverse-Ising physics into penalised linear regression. |

---

## 4 Linear Classification

### Chapters

* **Bishop-24 Ch 5** – Logistic-sigmoid networks and soft-max regression.
* **Murphy-22 Ch 9–10** – Fisher-LDA and logistic regression foundations.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S28 | [arXiv 1906.02481](https://arxiv.org/abs/1906.02481) | Linear classifiers endowed with symmetry constraints, elevating the basic perceptron into equivariant spaces. |

---

## 5 Neural Networks & Deep Learning

### Chapters

* **Bishop-24 Ch 6, 8, 10** – Multilayer perceptrons, back-prop,  and CNNs.
* **Goodfellow-16 Ch 6–9** – Deep feed-forward, regularisation,  and convolutional networks.
* **Murphy-22 Ch 11–13** – MLP, CNN and sequence nets.
* **Murphy-23 Ch 16–17** – Very-deep architectures and Bayesian NNs.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S6  | [arXiv 2008.01540](https://arxiv.org/abs/2008.01540)                              | Argues cosmological simulation encoded as NN. Underscores expressive power.      |
| S7  | [Nature Phys 2020](https://www.nature.com/articles/s41567-020-0929-2)             | Gives physicists an architect’s view of DL layers. Complements Goodfellow’s engineering view.        |
| S10 | [arXiv 2301.00942](https://arxiv.org/abs/2301.00942)                              | Solves computational-physics PDEs with generic DNNs. Depth pays off in science workloads.       |
| S29 | [arXiv 2002.12880](https://arxiv.org/abs/2002.12880)                              | CNNs expanded to Lie-group symmetries. See Bishop’s translation-equivariance. |
| S30 | [arXiv 2104.13478](https://arxiv.org/abs/2104.13478)                              | Geometric DL road maps connecting CNN to manifolds and graphs.                      |
| S31 | [arXiv 1906.01563](https://arxiv.org/abs/1906.01563)                              | Embeds Hamiltonian mechanics injecting physics priors into deep feed-forward models.   |
| S32 | [arXiv 2010.13581](https://arxiv.org/abs/2010.13581)                              | Extends Hamiltonian nets to higher-order systems, pushing physics-aware architectures.          |
| S33 | [arXiv 2003.04630](https://arxiv.org/abs/2003.04630)                              | Neural networks via Lagrangian dynamics.             |
| S34 | [arXiv 2202.04836](https://arxiv.org/abs/2202.04836)                              | Adds constraint handling to Hamiltonian NNs. Robotics and molecule simulation.               |
| S35 | [Nature Rev Phys 2021](https://www.nature.com/articles/s42254-021-00314-5)        | Reviews of physics-informed DL field. Domain priors.X-IML                   |
| S36 | [arXiv 2203.16797](https://arxiv.org/abs/2203.16797)                              | Recipes for engineering PIML systems.                                            |
| S37 | [arXiv 2304.14994](https://arxiv.org/abs/2304.14994)                              | U-Nets as neural surrogates for expensive PDE solvers.                                |
| S38 | [arXiv 2309.01909](https://arxiv.org/abs/2309.01909)                              | Reinforcement learning with physics constraints.                 |
| S41 | [Phys Rev E 98](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.98.062120) | Path integral analysis wide-network learning trajectories. Quantum mechanics and back prop |
| S43 | [arXiv 1910.00019](https://arxiv.org/abs/1910.00019)                              | Neural tangent kernel theory for infinite-width MLPs.                           |

---

## 6 Kernel Methods & Gaussian Processes

### Chapters

* **Murphy-22 Ch 14** – SVMs, kernel trick and kernel ridge.
* **Murphy-23 Ch 18** – Full Bayesian treatment of Gaussian processes.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S18 | [arXiv 2306.02108](https://arxiv.org/abs/2306.02108)              | Random-matrix theory for spectrum of GP kernels. Inductive bias. |
| S19 | [RMT4ML notes 2023](https://zhenyu-liao.github.io/pdf/RMT4ML.pdf) | Pedagogy-first walk through of RMT diagnosis of kernel learning dynamics.                    |

---

## 7 Regularisation & Ensemble Learning

### Chapters

* **Goodfellow-16 Ch 7** – Dropout, L1/L2, data augmentation.
* **Bishop-24 Ch 9** – Modern view: batch-norm, residual paths, double-descent.
* **Murphy-22 Ch 16 & 18** – k-NN sparsity plus tree/boosting ensembles.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S13 | [StatMechDeep PDF](https://ganguli-gang.stanford.edu/pdf/20.StatMechDeep.pdf)         | Free-energy landscapes view of regularisation flattening of minima.                                     |
| S14 | [Physica A 2023](https://www.sciencedirect.com/science/article/pii/S0378437122007129) | Measures penalties sculpting loss surfaces.                     |
| S56 | [arXiv 1709.02470](https://arxiv.org/abs/1709.02470)                                  | Double-descent and phase-transitions theory, giving statistical-physics view of ensembles. |

---

## 8 Graphical Models & Structured Probability

### Chapters

* **Bishop-24 Ch 11** – Factor graphs, HMMs, autoregressive densities.
* **Murphy-23 Ch 4 & 30** – Modern structure-learning and graph inference.
* **PRML-06 Ch 8–10** – The classic directed + undirected PGM treatment.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S39 | [Spin-Glass Book](http://www.stat.ucla.edu/~ywu/research/documents/BOOKS/SpinGlassInformation.pdf) | Probabilistic inference as energy minimisation.   |
| S42 | [arXiv 1901.10416](https://arxiv.org/abs/1901.10416)                                               | Statistical field theory methods and deep nets. |
| S44 | [Springer SFT-NN 2020](https://link.springer.com/book/10.1007/978-3-030-46444-8)                   | Monograph-length bridge between field theory and deep nets.                         |
| S45 | [arXiv 2109.13247](https://arxiv.org/abs/2109.13247)                                               | Reviews DL–QFT correspondence.                                         |
| S46 | [arXiv 2106.10165](https://arxiv.org/abs/2106.10165)                                               | Effective-field theory methods I.                                |
| S47 | [arXiv 2008.08601](https://arxiv.org/abs/2008.08601)                                               | Effective-field theory methods II.                   |
| S48 | [arXiv 2102.09449](https://arxiv.org/abs/2102.09449)                                               | QFTs as NN.                          |
| S49 | [arXiv 1812.09345](https://arxiv.org/abs/1812.09345)                                               | MSRJD and Onsanger Machlup.         |
| S50 | [arXiv 2212.11811](https://arxiv.org/abs/2212.11811)                                               | Renormalization and group flows.                       |
| S51 | [arXiv 2108.01403](https://arxiv.org/abs/2108.01403)                                               | RG acting as a hierarchy of probabilistic graphs.                              |

---

## 9 Dimensionality Reduction & Latent Variables

### Chapters

* **Bishop-24 Ch 16 & 19** – PCA, FA, ICA and autoencoders/VAEs.
* **Goodfellow-16 Ch 13–14** – Linear factor models and AEs in DL style.
* **Murphy-22 Ch 20** – t-SNE, Isomap, kernel PCA.
* **Murphy-23 Ch 27–28, 32** – Discovery & representation learning.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S54 | [arXiv 1610.09733](https://arxiv.org/abs/1610.09733) | PCA spectra RG flows: dimensionality reduction and scale-finding. |
| S55 | [J. Stat. Phys. 2017](https://link.springer.com/article/10.1007/s10955-017-1770-6) | PCA–RG connections in biological and financial data. |

---

## 10 Deep Generative Models

### Chapters

* **Bishop-24 Ch 15, 17, 18, 20** – Discrete latents, GANs, flows and diffusion.
* **Goodfellow-16 Ch 20** – Early 2016 survey of deep generators.
* **Murphy-23 Ch 20–26** – Probabilistic view of VAEs, GANs, and Diffusion.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S3 | [PIL tutorial PDF](https://wangleiphy.github.io/lectures/PILtutorial.pdf) | VAEs and denoising AEs. Code example tutorial |
| S20 | [arXiv 2006.11239](https://arxiv.org/abs/2006.11239) | Invents DDPMs. |
| S21 | [arXiv 2011.13456](https://arxiv.org/abs/2011.13456) | Score-based SDE sampling and Itô calculus. |
| S25 | [arXiv 2010.00029](https://arxiv.org/abs/2010.00029) | RG steps as an unsupervised flow. |
| S52 | [arXiv 1503.03585](https://arxiv.org/abs/1503.03585) | Early nonequilibrium: Foreshadowes modern score-matching diffusions. |

---

## 11 Approximate Inference & Normalising Flows

### Chapters

* **Bishop-24 Ch 7** – SGD, Adam, line-search, initialisation.
* **Murphy-23 Ch 7, 10 & 23** – Inference overview, variational Bayes, modern flows.
* **Goodfellow-16 Ch 8 & 19** – Optimisation details. Deep energy models.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S17 | [arXiv 1806.07366](https://arxiv.org/abs/1806.07366) | Neural ODEs. Continuous-time optimisation and invertible flows. |
| S31–S34 | see §5 | Hamiltonian/Lagrangian NNs as volume-preserving flows for Bayesian inference. |
| S40 | [arXiv 1603.01880](https://arxiv.org/abs/1603.01880) | Chaos in neural ODE training. Queries flow stability. |
| S41 | [Phys Rev E 98](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.98.062120) | Path-integral methods to approximate posterior dynamics of wide nets. |

---

## 12 Sampling & Monte-Carlo Methods

### Chapters

* **Bishop-24 Ch 14** – Metropolis, slice, Gibbs, HMC.
* **Murphy-23 Ch 11–13** – MC integration, adaptive MCMC, SMC.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S15 | [Andrieu et al. 2003](https://www.cs.ubc.ca/~arnaud/andrieu_defreitas_doucet_jordan_intromontecarlomachinelearning.pdf) | Classic tutorial. |
| S16 | [arXiv 2402.09598](https://arxiv.org/abs/2402.09598) | Modern review: Updates Bishop’s 2006 toolkit. |

---

## 13 Sequence & Time-Series Learning

### Chapters

* **Goodfellow-16 Ch 10** – RNN fundamentals.
* **Bishop-24 Ch 12** – Transformers and self-attention.
* **Murphy-23 Ch 8 & 29** – Kalman/LDS and modern state-space nets.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S57 | [Cardiff 2015](https://orca.cardiff.ac.uk/id/eprint/90458/) | Pioneers CNN inference on raw gravitational-wave time series. Beats matched filtering. |
| S58 | [arXiv 1710.07092](https://arxiv.org/abs/1710.07092) | Uses HMMs for continuous GW tracking. Mirrors hidden-state example. |
| S59 | [arXiv 1911.09083](https://arxiv.org/abs/1911.09083) | Deploys DL sequence nets to reduce GW detection latency. |
| S60 | [arXiv 2001.02515](https://arxiv.org/abs/2001.02515) | RNNs can emulate evolution of Einstein equations. |
| S61 | [arXiv 2110.08901](https://arxiv.org/abs/2110.08901) | Builds surrogates GW waveforms. |
| S62 | [IOP 2021](https://iopscience.iop.org/article/10.1088/2632-2153/abb93a) | Combines spectrogram preprocessing with CNN classifiers for GW bursts. |
| S63 | [arXiv 2201.01644](https://arxiv.org/abs/2201.01644) | Learns exact GR solutions. |
| S64 | [arXiv 2210.07299](https://arxiv.org/abs/2210.07299) | Compresses full numerical-relativity waveforms with autoencoding, reducing storage 100×. |

---

## 14 Decision-Making, Causality & Frontier Topics

### Chapters

* **Murphy-23 Ch 33–36** – Interpretability, decision theory, RL and causal inference.
* **Goodfellow-16 Ch 11–12** – Practical methodology and application case-studies.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S52 | [arXiv 1503.03585](https://arxiv.org/abs/1503.03585) | Learning as a nonequilibrium process,. |
| S53 | [arXiv 1906.10228](https://arxiv.org/abs/1906.10228) | Statistical physics view of RL. |

---

