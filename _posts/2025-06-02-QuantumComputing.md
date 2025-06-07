---
layout:   post
title: "Quantum Computing"
date: 2025-06-02 10:00:00 +0800
categories: [Computational Finance]
tags: [Quantum Computing, Quantitative Finance, Quantum Field Theory, Machine Learning, Computational Finance]
math:       true        # enable KaTeX
---
# Notes on Quantum Computing (Draft)

## Abstract
A brief survey of quantum computing is provided. Following an overview, a section on the mathematical foundations precedes a section on engineering quantum architectures.  Quantum information theory, theory of quantum computation,  and quantum computational complexity are included in the section on mathematical foundations. Three application domains are then considered: 1. Quantum physics (*viz* many-body theory & quantum fields), 2. Machine learning, and 3. Quantitative finance.

**To be continued ...**

### 1. Overview

| ID | Source | Notes |
|---|---|---|
| S1   | [1981 Feynman Quantum Computation](https://catonmat.net/ftp/simulating-physics-with-computers-richard-feynman.pdf) | Feynman argues that classical computers cannot efficiently simulate quantum systems and proposes the conceptual framework for a quantum computer. |
| S2   | [1984 Deutsch Quantum Computation](https://www.cs.princeton.edu/courses/archive/fall04/cos576/papers/deutsch85.pdf)                  | Deutsch introduces the notion of a universal quantum computer and shows how quantum mechanics can be harnessed to perform computations beyond classical capabilities. |
| S3   | [2000 Intro Quantum Computing](https://arxiv.org/abs/quant-ph/9809016)                         | This survey provides an accessible introduction to the principles of quantum computation, including qubits, quantum gates, and basic algorithms. |
| S4   | [2001 Kleinert QC](https://arxiv.org/abs/quant-ph/0106095)                                   | Kleinert explores path-integral methods in quantum information theory and their applications to quantum computing frameworks. |
| S5   | [2008 Geometry QC](https://arxiv.org/abs/quant-ph/0701004)                                     | This work develops a geometric approach to quantum computation, illustrating how differential geometry techniques can optimize quantum gate design. |
| S6   | [2010 Quantum Computation Bohm](https://arxiv.org/abs/1012.4843)                        | The authors examine quantum computational models from a Bohmian mechanics perspective, discussing how hidden-variable interpretations influence algorithmic performance. |
| S7   | [2018 QCSupremacy](https://arxiv.org/abs/1809.07442)                                     | This paper proposes benchmarks for demonstrating quantum supremacy and analyzes noise requirements for near-term quantum devices. |
| S8   | [2018 Quantum Circuits](https://arxiv.org/abs/1810.08277)                                 | The authors present a detailed study of quantum circuit synthesis techniques aimed at reducing gate depth in noisy intermediate-scale quantum (NISQ) processors. |

---

### 2. Foundations

| ID | Source | Notes |
|---|---|---|
| S9   | [2002 Mermin](https://www.cambridge.org/core/books/quantum-computer-science/66462590D10C8010017CF1D7C45708D7#fndtn-information) | Mermin offers a concise overview of the mathematical foundations underlying quantum computer science, including logic, linear algebra, and complexity considerations. |
| S10   | [2002 Oskin](https://homes.cs.washington.edu/~oskin/quantum-notes.pdf)          | Lecture notes as a companion to Nielsen and Chuang |
| S11   | [2007 Mermim Quantum Computation](https://arxiv.org/abs/quant-ph/0207118) | In this extended version, Mermin revisits quantum computation topics with additional mathematical rigor, clarifying error correction schemes and entanglement measures. |
| S12   | [2010 Nielsen Chuang](https://www.cambridge.org/highereducation/books/quantum-computation-and-quantum-information/01E10196D0A682A6AEFFEA52D53BE9AE#overview) | Nielsen & Chuang systematically develop the linear-algebraic and algorithmic foundations of quantum computing and quantum information theory. |
| S13   | [2012 IntroTQC](https://www.cambridge.org/core/books/introduction-to-topological-quantum-computation/F6C4B2C9F83E434E9BF3F73E492231F0#fndtn-information) | This work introduces the mathematical framework of topological quantum computation, focusing on anyonic systems and braiding statistics. |
| S14   | [2016 Aaronson Survey](https://arxiv.org/pdf/1607.05256)             | Scott Aaronson surveys computational complexity results related to quantum computing, discussing classes such as BQP and QMA.                     |
| S15   | [2018 Quantum Information Theory](https://www.cambridge.org/core/books/theory-of-quantum-information/AE4AA5638F808D2CFEB070C55431D897#fndtn-information) | This text develops rigorous proofs for key theorems in quantum information theory, such as the quantum coding theorem and entropic inequalities. |
| S16   | [2018 Aaronson](https://www.scottaaronson.com/qclec/combined.pdf) | Aaronson’s comprehensive lecture notes cover quantum algorithms, complexity theory, and theoretical underpinnings of quantum supremacy experiments. |
| S17   | [2018 Witten](https://arxiv.org/abs/1805.11965)               | Witten explores classical and quantum information theory. |

---

### 3. Engineering

| ID | Source | Notes |
|---|---|---|
| S18   | [2010 Quantum Quenching](https://link.springer.com/book/10.1007/978-3-642-11470-0)           | This monograph examines quantum quenching protocols in condensed matter systems and their applications to quantum annealing hardware. |
| 19   | [2017 Quantum Annealing](https://arxiv.org/abs/1701.04579)                                   | The authors review the principles of quantum annealing devices, focusing on hardware implementations and benchmarking against classical heuristics. |
| S20   | [2018 PracticalQC](https://link.springer.com/book/10.1007/978-1-4842-4218-6)                  | This book provides hands-on guidance for programming and deploying quantum algorithms on current commercial quantum processors. |
| S21   | [2018 Quantum Annealing Spin Glass](https://arxiv.org/abs/1708.08885)                        | Investigates spin-glass models as benchmarks for quantum annealing machines, analyzing performance on combinatorial optimization tasks. |
| S22   | [2018 Quantum Internet](https://arxiv.org/abs/1810.08421)                                          | Proposes architectural designs for a quantum internet, detailing entanglement distribution protocols and error-corrected links. |
| S23   | [2018 Quantum Internet](https://arxiv.org/abs/1805.04360)                                           | This paper outlines the practical challenges of engineering a large-scale quantum network, including qubit transduction and repeater synchronization. |
| S24  | [2019 Quantum Supremacy](https://www.nature.com/articles/s41586-019-1666-5)                       | Google’s team demonstrates a 53-qubit superconducting processor performing a computational task in 200 seconds that would take the fastest classical supercomputer approximately 10,000 years. |
| S25  | [2021 GoogleTimeCrystal](https://arxiv.org/abs/2107.13571)                               | This report discusses Google’s experimental realization of discrete time crystals in a superconducting quantum processor and its implications for quantum information processing. |

---
### 4: Applications: Quantum Physics

| ID | Source | Notes |
|---|---|---|
| S26   | [2015 QCQFT](https://arxiv.org/abs/1503.08121)                                           | QCQFT investigates the intersection of quantum computing and quantum field theory by way of continuous variables. | 
| S27   | [2018 Simulating Quantum Fields  ](https://arxiv.org/abs/1811.10085)           | Considers the practical promises and challenges of Feynman's original vision    |
| S28   | [2018 QC Chemistry](https://arxiv.org/abs/1808.10402)           | Demonstrates how quantum algorithms can simulate molecular ground states more efficiently than classical methods, with applications to drug design.    |
| S29   | [2023 QC Many Body](https://arxiv.org/abs/2303.04850)           | Studies quantum algorithms for simulating many-body physics, focusing on fragmentation techniques to reduce circuit depth.                          |
| S30   | [2024 QC in High Energy](https://arxiv.org/abs/2307.03236)      | Investigates quantum computing approaches to lattice gauge theories and high-energy physics simulations, assessing resource requirements.             |
                   |

---

### 5: Applications: Machine Learning

| ID | Source | Notes |
|---|---|---|
| S31   | [2014 QML](https://arxiv.org/abs/1409.3097)                                                               | Introduces core concepts of quantum machine learning, covering quantum data representation and basic variational algorithms.                                 |
| S32   | [2014QuantumMachineLearning](https://www.sciencedirect.com/book/9780128009536/quantum-machine-learning#book-info) | This edited volume collects foundational chapters on quantum algorithms for supervised and unsupervised learning, including kernel methods.                 |
| S33   | [2015 QML](https://arxiv.org/abs/1512.02900)                                                               | Presents a variational quantum algorithm for classification tasks and benchmarks its performance on small-scale datasets.                                    |
| S34   | [2017 QC Hopfield](https://arxiv.org/abs/1711.11240)                                                       | Develops a quantum version of Hopfield associative memory, showing exponential capacity improvements over classical counterparts.                            |
| S35   | [2017 QML](https://arxiv.org/abs/1707.08561)                                                               | Surveys architectures for quantum neural networks, including feedforward, convolutional, and recurrent quantum models.                                       |
| S36   | [2017 SurveyQuantumLearning](https://arxiv.org/abs/1701.06806)                                             | Provides a comprehensive review of quantum learning theory, touching on PAC learnability and sample-complexity bounds in quantum settings.                   |
| S37   | [2018 QML](https://arxiv.org/abs/1611.09347)                                                               | Introduces quantum algorithms for clustering and dimensionality reduction, demonstrating proof-of-principle implementations.                                  |
| S38   | [2018 QML BoltzmanMachine](https://arxiv.org/abs/1601.02036)                                               | Proposes training a quantum Boltzmann machine using a variational quantum circuit, highlighting potential quantum-speedup in sampling.                       |
| S39   | [2018 QC Tensor Networks](https://arxiv.org/abs/1803.11537)                                                | Explores tensor-network methods for representing variational quantum circuits and their use in scalable quantum machine learning.                            |
| S39  | [2024 QMLHealthcare](https://ieeexplore.ieee.org/document/10398184)                                         | Reviews recent advances in quantum machine learning for healthcare applications, including diagnostic imaging and drug-discovery pipelines.                  |

---

### 6: Applications: Quantitative Finance

| ID | Source | Notes |
|---|---|---|
| S40   | [2018 QC Finance](https://arxiv.org/abs/1811.03975)                                              | Examines how quantum algorithms can accelerate option pricing and portfolio optimization, comparing performance to classical Monte Carlo methods. |
| S41   | [2018 QC Finance Monte Carlo](https://arxiv.org/abs/1805.00109)                                   | Demonstrates a quantum-accelerated Monte Carlo algorithm for computing risk measures in financial portfolios with provable quadratic speedups. |
| S42   | [2019 QC Finance](https://arxiv.org/abs/1807.03890)                                              | Surveys emerging quantum computing applications in finance, including credit scoring, derivative pricing, and fraud detection.               |
| S43   | [2020 Optimal Trading Quantum Annealing](https://arxiv.org/abs/1508.06182)                       | Proposes a quantum annealing framework for constructing optimal trading strategies under transaction-cost constraints.     

