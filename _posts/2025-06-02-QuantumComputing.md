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

Research notes on quantum computing are provided, organized as an idiosyncratic guide to the literature that mirrors the structure of the subject. Following an overview of the field's conceptual origins---from Feynman's 1982 proposal through the formalization of quantum computational supremacy---the mathematical foundations are developed through pedagogical and reference texts spanning quantum information theory, computational complexity, and algorithmic theory. A section on engineering quantum architectures covers hardware implementations, quantum annealing, and networking. Three application domains are then surveyed: quantum simulation of physical systems (many-body theory and quantum fields), machine learning, and quantitative finance. The notes draw on 43 primary sources spanning 1982--2024, with particular attention to the relationships between sources and the gaps in existing coverage. These notes provide the framework for the quantum computing projects in the accompanying repository.

---

## 1. Overview

The intellectual origins of quantum computing lie in a simple observation about the structure of physical theory. Classical simulation of quantum systems encounters a fundamental resource barrier: the state space of $N$ quantum particles scales exponentially with $N$, so that any direct classical representation requires tracking an exponentially growing number of configurations. The question that launched the field was whether this barrier could be circumvented by building computers whose degrees of freedom are themselves quantum mechanical.

### 1.1 Feynman's Proposal

The founding document is Feynman's 1982 paper, "Simulating Physics with Computers" [S1], delivered as a keynote at the Physics of Computation conference (the paper is conventionally cited as 1981 from the conference date, though the publication appeared in 1982). Feynman's argument proceeds along several lines that remain instructive. He distinguishes between *imitating* time evolution (as in cellular automata) and *simulating* it, and he insists on local interconnection in any realistic computational model. The central technical observation is that probability amplitudes---which can be negative, unlike classical probabilities---are the fundamental departure from classical probabilistic computation.

Feynman makes this concrete through the EPR paradox and Bell inequalities. For two entangled photons measured at 30° separation, quantum mechanics predicts a correlation probability of $\cos^2(30°) = 3/4$, while any classical hidden-variable model is bounded by $2/3$. No classical probabilistic computer can reproduce quantum correlations. The explicit question Feynman raises---whether a *universal quantum simulator* exists---would be addressed formally by Deutsch three years later.

The paper remains remarkably accessible and rewards reading in full. Its rhetorical strategy---moving from physical systems to computational models, rather than the reverse---established the simulation-first perspective that continues to motivate much of the field.

### 1.2 Deutsch and the Universal Quantum Computer

Deutsch's 1985 paper, "Quantum Theory, the Church--Turing Principle and the Universal Quantum Computer" [S2], formalizes what Feynman left as a conjecture. Deutsch introduces a quantum variant of the Church--Turing thesis: *every finitely realizable physical system can be perfectly simulated by a universal quantum computer operating by finite means*. The paper establishes the theoretical foundation for quantum parallelism arising from superposition and connects it to the circuit model that would become standard.

A note on the bibliography: the original page lists this as "1984," but the paper was published in 1985. The linked PDF, hosted at Princeton's CS department, is Deutsch's original. Readers approaching from a computer science background may find it useful to trace the line from Deutsch's universality argument through the Deutsch--Jozsa algorithm to the circuit-model formalism of later textbooks.

### 1.3 Surveys and Alternative Perspectives

The remaining overview sources serve as entry points from different vantage points.

Rieffel and Polak [S3] (arXiv:quant-ph/9809016, updated 2000) provide an accessible survey aimed at computer scientists. The paper covers qubits, gates, key protocols (teleportation, dense coding), and gives high-level overviews of Shor's and Grover's algorithms, concluding with a discussion of quantum error correction. It functions well as an "index" to deeper treatments and is a natural starting point for readers without prior exposure to the formalism.

The Haba and Kleinert paper [S4] (arXiv:quant-ph/0106095, 2001) requires careful annotation. The original page describes it as exploring "path-integral methods in quantum information theory," but this materially mischaracterizes the paper. It is a brief (3-page) note proposing a classical stochastic differential-equation construction whose averaged dynamics reproduce a Schrödinger equation for certain systems (harmonic oscillator, then generalized potentials). The paper is better understood as a "dequantization" curiosity---an attempt to simulate quantum behavior with classical stochastic dynamics---rather than a contribution to quantum computing *per se*. Its relevance to this survey is primarily as a counterpoint: it illustrates the question of *when and whether* classical stochastic methods can substitute for quantum computation, a question that has grown more significant with the dequantization results of Tang and others in the machine learning context (see Section 5).

Nielsen, Dowling, Gu, and Doherty [S5] (arXiv:quant-ph/0701004) develop a differential-geometric viewpoint on quantum circuit complexity. The key idea is to treat quantum computation as geodesic motion on a manifold of unitary operators equipped with appropriate cost metrics. This provides tools for reasoning about lower bounds on circuit depth and connects quantum compilation to optimal control theory. The framing as "optimizing quantum gate design" (as on the original page) is directionally correct but somewhat imprecise; the contribution is to circuit *complexity* analysis rather than hardware engineering.

Roser [S6] (arXiv:1012.4843, 2010) examines quantum computation from the de Broglie--Bohm pilot-wave picture. This is an interpretational exercise: it explores standard quantum computational phenomena through Bohmian mechanics and asks what the hidden-variable ontology suggests about the source of quantum speedups. The paper does not yield new algorithms or complexity results; interpretational compatibility with quantum computation is established, but readers should not expect algorithmic consequences.

Harrow and Montanaro [S7] (arXiv:1809.07442, 2018) provide a survey of what "quantum supremacy" (now often called "quantum advantage") means as a theoretical and experimental concept. The paper analyzes evidence standards, candidate tasks (particularly random circuit sampling), and noise thresholds for near-term devices. It preceded Google's 2019 experimental demonstration [S24] and provides the conceptual framework for interpreting that result.

Ossorio-Castillo and Tornero [S8] (arXiv:1810.08277, updated 2025) is a self-contained, mathematically oriented exposition of the quantum circuit model. It covers foundational definitions, complexity class discussions (including BQP), and standard algorithmic building blocks. The original page describes this as "quantum circuit synthesis techniques reducing gate depth for NISQ," which is not the paper's thrust. It is expository rather than a contribution to compilation or synthesis. Readers seeking gate-depth reduction techniques for NISQ processors should look to the variational quantum eigensolver literature and dedicated compilation papers.

### 1.4 Summary Table: Overview Sources

| ID | Source | Year | Core Contribution |
|----|--------|------|-------------------|
| S1 | Feynman | 1982 | Exponential classical simulation barrier; proposes quantum computer |
| S2 | Deutsch | 1985 | Universal quantum computer; quantum Church--Turing principle |
| S3 | Rieffel & Polak | 2000 | Accessible CS-oriented survey of qubits, gates, algorithms |
| S4 | Haba & Kleinert | 2001 | Classical stochastic simulation of quantum dynamics (dequantization curiosity) |
| S5 | Nielsen *et al.* | 2006 | Geometric viewpoint on circuit complexity via unitary manifolds |
| S6 | Roser | 2010 | Bohmian mechanics interpretation of quantum computation |
| S7 | Harrow & Montanaro | 2018 | Supremacy definitions, evidence standards, sampling tasks |
| S8 | Ossorio-Castillo & Tornero | 2018 | Math-forward exposition of the quantum circuit model |

---

## 2. Foundations

The mathematical foundations of quantum computing draw from linear algebra, information theory, computational complexity, and the formalism of quantum mechanics itself. The sources in this section range from compact pedagogical introductions to comprehensive reference texts and specialized surveys.

### 2.1 Pedagogical Texts

Mermin's *Quantum Computer Science* [S9] (Cambridge, 2007) is a compact, idiosyncratic treatment that develops the mathematical foundations without requiring prior physics background. Mermin emphasizes logic, linear algebra over Hilbert spaces, and measurement theory with characteristic clarity. The book works well as a first pass through the formalism for readers comfortable with linear algebra but unfamiliar with quantum mechanics.

The Oskin lecture notes [S10] (University of Washington, 2002) serve as a companion to Nielsen and Chuang and provide a computer science--oriented treatment in approximately 56 pages. The notes are notable for including explicit numerical resource-estimation calculations for fault-tolerant quantum computation. One example is particularly instructive: assuming a decoherence rate $\lambda = 10^{-6}$, without error correction only approximately 4 qubits can be reliably factored. With $k = 5$ levels of recursive error correction (concatenation), factoring 1024-bit numbers becomes possible in principle, but at enormous overhead: 16,807 physical qubits per logical qubit and approximately $8.4 \times 10^{10}$ physical gates per logical gate. These numbers provide a concrete sense of the engineering challenge that separates theoretical algorithms from physical implementation.

The notes cover the four postulates of quantum mechanics formulated for qubits, entanglement and EPR pairs, teleportation and superdense coding, the Deutsch--Jozsa algorithm, Bloch sphere representations, universal gate sets ($H$, $X$, $T$, CNOT), Shor's algorithm (both direct and phase-estimation formulations), Grover's search with $O(\sqrt{N})$ complexity, and quantum error correction including 3-qubit codes, the 9-qubit Shor code, and the 7-qubit Steane code.

Mermin's arXiv paper "From Cbits to Qbits" [S11] (arXiv:quant-ph/0207118, 2002) is a teaching-oriented exposition that walks from classical bits to qubits, again emphasizing measurement and linear algebra. The original page labels this as "2007" and describes it as providing "additional rigor on error correction and entanglement measures"; the paper is actually from 2002 and is primarily pedagogical rather than a technical deep-dive on quantum error correction. It complements the textbook [S9] by taking a somewhat different pedagogical path through the same foundational material.

### 2.2 Comprehensive References

Nielsen and Chuang's *Quantum Computation and Quantum Information* [S12] (Cambridge, 10th anniversary edition 2010) is the canonical textbook of the field. It systematically develops quantum computing and quantum information theory from linear-algebraic foundations, covering quantum circuits, standard algorithms (Shor, Grover), quantum error correction, quantum cryptography, and physical implementations. Nearly every other source in this survey either builds on or reacts to the framework established here. For readers working through the present notes, Nielsen and Chuang serves as the primary reference for filling in details that the survey sources treat in compressed form.

Watrous's *The Theory of Quantum Information* [S15] (Cambridge, 2018) provides a rigorous development of quantum information theory---channels, entropy, coding theorems, capacity results---with full proofs. This is an *information theory* text rather than a *computation* text, and the distinction matters: readers seeking algorithmic content should look elsewhere, but those needing the measure-theoretic and operator-algebraic underpinnings of quantum information will find this indispensable.

### 2.3 Topological Quantum Computation

Pachos's *Introduction to Topological Quantum Computation* [S13] (Cambridge, 2012) develops the mathematical framework of anyonic systems and braiding statistics. The topological approach to quantum computation offers intrinsic protection against local errors: information is encoded in global topological properties of the system that are insensitive to local perturbations. This is the theoretical basis for Microsoft's research program using Majorana fermions as a hardware platform.

The key idea is that in two spatial dimensions, the exchange statistics of particles are governed by the braid group rather than the permutation group. Non-Abelian anyons---whose exchange operations do not commute---can encode quantum information in their fusion channels, and computation proceeds via braiding operations. The protection against decoherence is topological rather than active (as in concatenated error correction codes), which in principle reduces the overhead required for fault tolerance. The practical challenge is fabricating systems that host non-Abelian anyons with sufficient control and coherence.

### 2.4 Complexity Theory

Aaronson's survey, "The Complexity of Quantum States and Transformations" [S14] (arXiv:1607.05256, 2016), provides the complexity-theoretic anchor for this section. It discusses complexity classes including BQP (bounded-error quantum polynomial time) and QMA (quantum Merlin--Arthur), their relationships to classical classes P, NP, and PSPACE, and extends to topical excursions into quantum money and black-hole information. The paper is structured as a survey that readers can sample by section according to their interests.

The central complexity-theoretic question is whether BQP $\neq$ BPP---that is, whether quantum computers can efficiently solve problems that classical probabilistic computers cannot. This remains unresolved as a formal complexity-theoretic statement (it would imply P $\neq$ PSPACE), but the evidence from specific algorithms (Shor's, Grover's, simulation algorithms) and from supremacy experiments strongly suggests an affirmative answer.

Aaronson's lecture notes from UT Austin [S16] (2018) provide a comprehensive pedagogical treatment covering quantum algorithms, complexity theory, and the theoretical underpinnings of supremacy experiments. Notable coverage includes Bell inequalities, Wiesner's quantum money scheme, BB84 quantum key distribution, superdense coding (transmitting 2 classical bits via 1 qubit plus preshared entanglement), interpretations of quantum mechanics (Copenhagen, Many-Worlds, decoherence theory), and the quantum Zeno effect. Aaronson emphasizes a subtle point: quantum mechanics maintains *locality* but violates *local realism*---and the Extended Church--Turing Thesis (that classical computers can efficiently simulate all physical systems) appears to be false, with quantum computing serving as the counterexample.

### 2.5 Information-Theoretic Foundations

Witten's "A Mini-Introduction to Information Theory" [S17] (arXiv:1805.11965, 2018) provides a characteristically elegant treatment of classical and quantum information measures: entropy, relative entropy, mutual information, and their quantum generalizations. The paper brings insights from mathematical physics to bear on information-theoretic questions and serves as a bridge between the physics-oriented and information-theoretic perspectives on quantum computation. The entropic tools introduced here connect to several later topics: channel capacity (relevant to quantum networking in Section 3), quantum learning theory (Section 5), and quantum thermodynamics.

### 2.6 Summary Table: Foundation Sources

| ID | Source | Year | Type | Core Contribution |
|----|--------|------|------|-------------------|
| S9 | Mermin | 2007 | Textbook | Compact QCS foundations; logic, linear algebra, complexity |
| S10 | Oskin | 2002 | Lecture notes | CS companion to Nielsen & Chuang; explicit QEC overhead calculations |
| S11 | Mermin | 2002 | Pedagogical paper | "Cbits to Qbits"; teaching-oriented exposition |
| S12 | Nielsen & Chuang | 2010 | Textbook | Canonical comprehensive reference |
| S13 | Pachos | 2012 | Textbook | Topological QC; anyons, braiding, fault tolerance |
| S14 | Aaronson | 2016 | Survey | Complexity classes BQP, QMA; quantum money to black holes |
| S15 | Watrous | 2018 | Textbook | Rigorous quantum information theory; channels, entropy, coding |
| S16 | Aaronson | 2018 | Lecture notes | Algorithms, complexity, Bell inequalities, interpretations |
| S17 | Witten | 2018 | Expository paper | Classical and quantum information measures |

---

## 3. Engineering

The engineering of quantum computing systems encompasses hardware implementations across several physical platforms, quantum annealing as an alternative computational paradigm, and the nascent development of quantum networking infrastructure. The sources collected here span from physics-oriented condensed matter treatments to practitioner-oriented programming guides.

### 3.1 Quantum Annealing and Condensed Matter

*Quantum Quenching, Annealing and Computation* [S18] (Springer, 2010) examines quantum quenching protocols in condensed matter systems and their relationship to quantum annealing as a computational paradigm. The book connects nonequilibrium dynamics and quench phenomena to the design of annealing hardware. Readers should note the distinction between two related but separable goals: (i) quantum annealing as an optimization technique (where the computational goal is primary) and (ii) quench dynamics as many-body physics (where the physical phenomena are of intrinsic interest). The annotation on the original page conflates these somewhat.

The paper "Quantum annealing amid local ruggedness and global frustration" [S19] (arXiv:1701.04579, 2017) is a focused study of how energy landscape structure---specifically local ruggedness and global frustration---affects quantum annealing performance. This is not a general hardware review, as the original page implies, but a targeted analysis of performance landscapes. The result is relevant to understanding when and why quantum annealing may or may not outperform classical optimization heuristics on specific problem classes.

*Practical Quantum Computing for Developers* [S20] (Springer, 2018) provides hands-on guidance for programming and deploying quantum algorithms on commercial quantum processors (IBM Q, Rigetti, and similar platforms). It complements the theory-heavy items in the foundations section and serves readers who wish to gain practical experience with actual quantum hardware.

"Benchmarking quantum annealers: the spin glass perspective" [S21] (arXiv:1708.08885, 2018) uses spin-glass models as benchmarks for quantum annealing machines, analyzing performance on combinatorial optimization tasks. The spin-glass perspective is natural because these models provide well-characterized, tunable instances of hard optimization problems. A methodological caution: performance claims for quantum annealers are sensitive to confounds including problem instance selection, parameter tuning, and the choice of classical baselines. This paper provides a framework for controlling these confounds.

### 3.2 Quantum Networking

Two papers address the engineering of quantum communication infrastructure. "Networking Challenges in Distributed Quantum Computing" [S22] (arXiv:1810.08421, 2018) frames distributed quantum computation as a systems and networking problem, discussing architectural constraints for entanglement distribution, teleportation-based links, and coordination protocols. The original page describes "error-corrected links" and concrete protocol designs; this overstates the paper's scope, which is better characterized as an *architectural discussion of challenges and tradeoffs* rather than a complete protocol specification.

"Quantum Internet: from Communication to Distributed Computing!" [S23] (arXiv:1805.04360, 2018) is a short invited overview (4 pages) relating quantum networking to distributed quantum computation and cloud computing frameworks. It highlights entanglement and teleportation as primitives and lists open challenges. Readers should treat it as a high-level roadmap rather than a technical design document.

### 3.3 Experimental Milestones

Google's quantum supremacy demonstration [S24] (Nature, 2019) used a 53-qubit superconducting processor (Sycamore) to perform a random circuit sampling task in 200 seconds, with the claimed classical comparison time of approximately 10,000 years on the world's fastest supercomputer. This represents a genuine experimental milestone, but the classical baseline has been the subject of significant debate. Multiple follow-on works (notably from IBM, and from classical simulation researchers using tensor-network methods) have argued that the best classical simulation time for the specific task chosen is substantially less than the original estimate, though still superpolynomial in asymptotic scaling. Any pedagogical treatment of this result should include this baseline controversy and the distinction between a specific experimental demonstration and a proof of asymptotic advantage.

The observation of discrete time crystals on a quantum processor [S25] (arXiv:2107.13571, 2021) demonstrates the use of Google's superconducting processor as a platform for many-body physics experiments. Time crystals are phases of matter exhibiting spontaneous breaking of discrete time-translation symmetry in periodically driven (Floquet) systems. This is an example of "physics on a quantum processor" rather than a computing application per se---the quantum device serves as a controlled many-body system for studying nonequilibrium phases of matter, which is closer to Feynman's original simulation vision than to the gate-model algorithmic paradigm.

### 3.4 Coverage Gaps in Engineering

The engineering section as curated has notable gaps. There is no systematic treatment of hardware modalities as a comparative set: superconducting qubits (IBM, Google), trapped ions (IonQ, Honeywell/Quantinuum), photonic systems (Xanadu, PsiQuantum), neutral atoms (QuEra, Pasqal), and spin qubits in semiconductors each have distinct characteristics in terms of coherence times, gate fidelities, connectivity, and scalability. A comprehensive engineering section would include at least one key review per modality.

Quantum error correction and fault tolerance receive only indirect treatment through the Oskin notes [S10] and Rieffel and Polak [S3]. Given that error correction is the central engineering challenge separating current NISQ devices from fault-tolerant quantum computers, this is a significant gap. Modern surface-code references and resource-estimation papers would strengthen this section substantially.

### 3.5 Summary Table: Engineering Sources

| ID | Source | Year | Core Contribution |
|----|--------|------|-------------------|
| S18 | *Quantum Quenching, Annealing and Computation* | 2010 | Condensed matter quench protocols and annealing |
| S19 | Quantum annealing landscapes | 2017 | Local ruggedness and frustration effects on annealing |
| S20 | *Practical Quantum Computing* | 2018 | Programming guides for commercial quantum processors |
| S21 | Spin glass benchmarks | 2018 | Benchmarking annealers with tunable hard instances |
| S22 | Quantum networking challenges | 2018 | Distributed QC architecture and constraints |
| S23 | Quantum internet overview | 2018 | Short roadmap for quantum communication infrastructure |
| S24 | Google supremacy experiment | 2019 | 53-qubit random circuit sampling demonstration |
| S25 | Google time crystals | 2021 | Discrete time-crystal observation on superconducting processor |

---

## 4. Applications: Quantum Physics

Quantum simulation of physical systems is the application domain closest to Feynman's original vision. The fundamental motivation is that quantum field theories and many-body quantum systems are exponentially expensive to simulate classically in general, but may be efficiently simulable on quantum hardware. The sources here span from conceptual investigations of the quantum computing--quantum field theory interface to practical assessments of near-term capabilities.

### 4.1 Quantum Computing and Quantum Field Theory

"Quantum Computing for Quantum Field Theory" [S26] (arXiv:1503.08121, 2015) explores the intersection of quantum computing and quantum field theory using continuous-variable approaches rather than the standard qubit (discrete-variable) framework. The continuous-variable approach is natural for field theories, where the fundamental degrees of freedom are fields defined on continuous spacetime. Readers should assess whether this paper functions as a "conceptual intersection" piece or a "practical algorithmic toolbox"---it leans toward the former.

Preskill's "Simulating Quantum Field Theory with a Quantum Computer" [S27] (arXiv:1811.10085, 2018), based on a talk at Lattice 2018, provides a high-level perspective on why QFT simulation matters, where classical methods fail (particularly the fermion sign problem in lattice QCD), and what quantum simulation might enable. Preskill's discussion connects to the broader resource-estimation literature: meaningful QFT calculations on quantum hardware will require substantial advances in both qubit count and error rates. The paper serves as a bridge between the lattice gauge theory community and the quantum computing community.

### 4.2 Quantum Chemistry

McArdle *et al.*, "Quantum Computational Chemistry" [S28] (arXiv:1808.10402, 2018), is a review of algorithms and near-term prospects for quantum chemistry applications. The original page describes this as "demonstrating" efficient ground-state simulation; more accurately, it is a *survey* of the algorithmic landscape, covering state preparation, the variational quantum eigensolver (VQE), quantum phase estimation, and error mitigation strategies. Quantum chemistry is often cited as the "killer application" for near-term quantum computers because classically intractable molecular simulations may become feasible at relatively modest qubit counts. The VQE serves as the primary near-term workhorse algorithm, while full quantum phase estimation remains a fault-tolerant-era target. The review clarifies the resource requirements for achieving "chemical accuracy" (~1 kcal/mol) on systems of practical interest.

### 4.3 Many-Body Physics and High-Energy Physics

"Quantum computing with and for many-body physics" [S29] (arXiv:2303.04850, 2023) is a broad modern review of many-body physics use cases, simulation strategies, and the feedback loop between many-body theory and quantum computing methods. The original page describes it as focused on "fragmentation techniques to reduce circuit depth"; while this is one topic the paper addresses, the scope is substantially broader and includes a survey of the full landscape of many-body quantum simulation.

The high-energy physics survey [S30] (arXiv:2307.03236, 2024) is a community-style overview of HEP use cases including lattice gauge theory simulation, event generation, optimization problems in detector design, and machine learning applications. It provides resource estimates for meaningful calculations and a mapping between HEP tasks and the corresponding algorithmic primitives (Hamiltonian simulation, quantum linear systems, sampling). This paper represents the current state of assessment regarding when quantum computers might contribute meaningfully to high-energy physics research.

### 4.4 Summary Table: Quantum Physics Applications

| ID | Source | Year | Core Contribution |
|----|--------|------|-------------------|
| S26 | QCQFT | 2015 | Continuous-variable QC--QFT interface |
| S27 | Preskill | 2018 | Why QFT simulation matters; sign problem; resource needs |
| S28 | McArdle *et al.* | 2018 | Review of quantum chemistry algorithms; VQE, QPE |
| S29 | Many-body QC | 2023 | Broad survey of many-body simulation strategies |
| S30 | HEP survey | 2024 | Community assessment of QC for high-energy physics |

---

## 5. Applications: Machine Learning

Quantum machine learning (QML) encompasses quantum algorithms for classical machine learning tasks, quantum-enhanced models, and the theoretical analysis of learning in quantum settings. This is a rapidly evolving subfield where early enthusiasm has been tempered by dequantization results showing that some claimed quantum speedups can be matched classically. The sources here span the early survey literature through recent application-oriented reviews, and several require corrected annotations relative to the original page.

### 5.1 Early Surveys and Foundations

Schuld, Sinayskiy, and Petruccione, "An Introduction to Quantum Machine Learning" [S31] (arXiv:1409.3097, 2014), is an early survey that frames QML in terms of (i) quantum speedups for subroutines (distance calculations, kernel evaluations), (ii) quantum analogs of probabilistic models, and (iii) early quantum neural network ideas. As a 2014-era survey, it predates the shift toward variational quantum circuits and kernel methods that reshaped the field after 2018. It remains useful as a snapshot of the conceptual landscape before the variational era.

The Elsevier edited volume *Quantum Machine Learning* [S32] (2014) collects foundational chapters on quantum algorithms for supervised and unsupervised learning, including kernel methods. It serves as a period document capturing early QML perspectives.

### 5.2 Algorithms, Models, and Architectures

Several sources in this section require corrected characterizations relative to the original page.

Adcock, Allen, *et al.* [S33] (arXiv:1512.02900, 2015) is titled "Advances in Quantum Machine Learning" and is a *review paper* covering multiple algorithms and learning settings. The original page describes it as "a variational quantum classifier benchmarked on small datasets," which is not what the paper does. It provides a broader survey of the QML landscape as of 2015. Readers seeking dedicated variational quantum classifier (VQC) work should look to the later literature, particularly Havlíček *et al.* (Nature, 2019) and the quantum kernel methods program.

Cao *et al.* [S34] (arXiv:1711.11240, 2017), "Quantum Neuron: an Elementary Building Block for Machine Learning on Quantum Computers," proposes a quantum neuron primitive with threshold-like behavior as a component for building higher-level QML models. The original page describes this as "a quantum Hopfield associative memory with exponential capacity improvements over classical counterparts." This is a material mischaracterization---the paper proposes a neuron-like building block, not an associative memory model. Readers interested in quantum Hopfield networks or quantum associative memories should seek dedicated references on those topics.

Ciliberto *et al.* [S35] (arXiv:1707.08561, 2017), "Quantum Machine Learning: a Classical Perspective," surveys QML ideas while explicitly emphasizing classical baselines and the importance of careful speedup claims. The original page frames this as "architectures for quantum neural networks (feedforward, CNN, RNN)," but the paper is broader and methodological---it is better understood as the "skeptical methodology" anchor in the QML literature, raising the question of whether claimed quantum advantages survive comparison with the best classical algorithms. This paper anticipates the dequantization results of Tang (2019) and subsequent work.

Arunachalam and de Wolf [S36] (arXiv:1701.06806, 2017) provide a theory-heavy survey of quantum learning theory, covering PAC learnability, sample complexity bounds in quantum settings, and the relationships between quantum and classical learning frameworks. This is mathematically dense and primarily of interest to readers working on the foundations of learning theory rather than practitioners building variational circuits.

Biamonte *et al.* [S37] (Nature 2017; arXiv:1611.09347) is a widely cited broad QML review covering quantum algorithms for linear algebra, clustering, kernels, and more. It positions QML within the broader quantum computing landscape and serves as a standard entry point to the field. Cross-referencing with [S35] for "speedup scrutiny" and with [S31] for early survey context is recommended.

### 5.3 Energy-Based and Tensor-Network Models

Amin *et al.* [S38] (arXiv:1601.02036, 2016), "Quantum Boltzmann Machine," proposes quantum Boltzmann machines using quantum Hamiltonians and analyzes learning and training in terms of energy-based models and thermal sampling. The original page describes "training using a variational quantum circuit," but this is not the paper's central framing. The quantum Boltzmann machine is formulated in terms of thermal equilibrium states of quantum Hamiltonians, not variational circuits. Readers interested in variational-circuit-based energy models should look to later work on quantum approximate optimization algorithms (QAOA) and variational quantum eigensolvers applied to learning problems.

Huggins *et al.* [S39a] (arXiv:1803.11537, 2018) explores tensor-network representations as tools for understanding and constructing variational quantum circuits. Tensor networks provide a bridge between classical machine learning (where they appear as restricted models of many-body states) and quantum circuits (where they describe the structure of shallow quantum computations). The connection is technically productive: tensor-network structure constrains the expressibility of variational ansätze and suggests principled circuit designs.

A 2024 IEEE review of QML for healthcare applications [S39b] addresses diagnostic imaging and drug-discovery pipelines. Access to the full text was limited (IEEE paywall), but the inclusion signals the expansion of QML into applied domains. An editorial note: the original page duplicates the label "S39" for these two distinct sources; one should be renumbered to avoid citation ambiguity.

### 5.4 The Dequantization Caveat

A cross-cutting issue in the QML literature deserves explicit mention. Beginning with Tang's 2019 dequantization results, it has been shown that several quantum machine learning speedups---originally claimed as exponential---can be matched or closely approximated by classical algorithms with access to the same data structures (specifically, sample-and-query access to the input data). This does not invalidate the QML research program, but it sharpens the question: for which learning tasks, under which access models, do quantum algorithms provide *genuine* advantage?

The present collection of sources addresses this question indirectly through [S35] (which emphasizes classical baselines) but would benefit from a dedicated dequantization reference to provide the reader with a balanced assessment of the state of the field.

### 5.5 Summary Table: Machine Learning Sources

| ID | Source | Year | Actual Contribution (Corrected) |
|----|--------|------|---------------------------------|
| S31 | Schuld *et al.* | 2014 | Early QML survey; subroutines, probabilistic models |
| S32 | *Quantum Machine Learning* (Elsevier) | 2014 | Edited volume; supervised/unsupervised algorithms |
| S33 | Adcock *et al.* | 2015 | QML review (not a variational classifier paper) |
| S34 | Cao *et al.* | 2017 | Quantum neuron primitive (not Hopfield memory) |
| S35 | Ciliberto *et al.* | 2017 | QML survey emphasizing classical baselines and skepticism |
| S36 | Arunachalam & de Wolf | 2017 | Quantum learning theory; PAC, sample complexity |
| S37 | Biamonte *et al.* | 2017 | Broad QML review; algorithms for linear algebra, kernels |
| S38 | Amin *et al.* | 2016 | Quantum Boltzmann machines via Hamiltonian models (not variational circuits) |
| S39a | Huggins *et al.* | 2018 | Tensor-network methods for variational circuits |
| S39b | IEEE healthcare QML | 2024 | QML for diagnostic imaging and drug discovery |

---

## 6. Applications: Quantitative Finance

Quantum computing applications in finance span option pricing, portfolio optimization, risk management, and combinatorial trading problems. The quadratic speedup from amplitude estimation (the quantum analog of Monte Carlo sampling) is the primary near-term algorithmic opportunity, while quantum annealing offers an alternative paradigm for optimization problems. Several source descriptions on the original page require correction.

### 6.1 Portfolio Optimization and Derivative Pricing

Egger *et al.* [S40] (arXiv:1811.03975, 2018) present quantum approaches to portfolio optimization, including problem encodings and algorithmic strategies. The original page frames this as a broad "option pricing + portfolio optimization" overview; it is more targeted than that and should not be conflated with the derivatives-focused Monte Carlo paper [S41].

Rebentrost, Gupt, and Bromley [S41] (arXiv:1805.00109, 2018), "Quantum Computational Finance: Monte Carlo Pricing of Financial Derivatives," shows how amplitude estimation yields a quadratic speedup in sample complexity for Monte Carlo--style derivative pricing, with European and Asian option examples. The original page describes this as computing "risk measures in financial portfolios"; the paper is primarily about derivative pricing rather than portfolio risk metrics. The quadratic speedup is provable under certain assumptions but comes with caveats about the depth of the quantum circuits required and the overhead of state preparation.

### 6.2 Surveys and Annealing-Based Trading

Orús *et al.* [S42] (arXiv:1807.03890, 2019) provide a broad survey covering multiple financial tasks---pricing, optimization, machine learning for finance---and practical constraints on near-term implementations. This is the most comprehensive survey in the collection and serves as a good entry point for readers interested in the financial applications landscape.

Rosenberg *et al.* [S43] (arXiv:1508.06182, 2015), "Solving the Optimal Trading Trajectory Problem Using a Quantum Annealer," maps a constrained optimal trading trajectory problem (with transaction costs and market impact) to a QUBO (Quadratic Unconstrained Binary Optimization) / Ising formulation suitable for quantum annealing. The original page labels this as "2020"; the arXiv preprint is from 2015. The paper demonstrates the *formulation* rather than a practical advantage over classical methods, and readers should note that the classical convex-optimization alternatives for these problem formulations are well-developed and efficient at scales far beyond current annealing hardware.

### 6.3 Finance Section Assessment

The finance sources collectively cover the three main algorithmic approaches: amplitude estimation for sampling speedups, variational/hybrid methods for optimization, and annealing for combinatorial formulations. The coverage is weighted toward surveys, which is appropriate for an introductory reading list. A notable gap is the absence of sources on quantum risk analysis (e.g., quantum algorithms for value-at-risk and conditional value-at-risk calculations) and on the practical resource estimates for achieving quantum advantage in financial applications---a question that remains open given the circuit depths required by amplitude estimation and the efficiency of classical alternatives.

### 6.4 Summary Table: Quantitative Finance Sources

| ID | Source | Year | Core Contribution |
|----|--------|------|-------------------|
| S40 | Egger *et al.* | 2018 | Quantum portfolio optimization; problem encodings |
| S41 | Rebentrost *et al.* | 2018 | Amplitude estimation for derivative pricing; quadratic speedup |
| S42 | Orús *et al.* | 2019 | Comprehensive survey of QC in finance |
| S43 | Rosenberg *et al.* | 2015 | QUBO formulation for optimal trading trajectories |

---

## 7. Summary

The 43 sources span four decades (1982--2024) and cover the field's conceptual origins, mathematical foundations, engineering challenges, and three significant application domains. The inclusion of both gate-model and annealing-based approaches provides breadth. The presence of canonical texts (Feynman, Deutsch, Nielsen and Chuang) alongside specialized surveys and recent applications papers gives the collection pedagogical range.

The interdisciplinary scope---connecting quantum physics simulation, machine learning, and quantitative finance---reflects the interdisciplinary intentions and character of *Projects in Scientific Computing* and positions quantum computing as a natural intersection point for the computational finance, quantum field theory, and numerical methods threads developed elsewhere in this work.


---

## 8. Connections to Other Chapters

Quantum computing intersects with several other chapters in *Projects in Scientific Computing*.

The **stochastic calculus** chapter provides the mathematical framework for understanding the dequantization results discussed in Section 5: classical stochastic processes with appropriate access models can sometimes match quantum sampling advantages. The relationship between quantum amplitude estimation and classical Monte Carlo methods (Section 6) is a direct connection to the probabilistic methods developed in the stochastic calculus and computational finance chapters.

The **quantum field theory** chapters---including QFT in curved spacetime, statistical field theory, and stochastic quantization---connect to the quantum simulation applications in Section 4. The sign problem in lattice QCD, which Preskill [S27] identifies as a key motivation for quantum simulation, is a manifestation of the broader difficulties with importance sampling in field theories with complex actions. The tensor-network methods discussed in Section 5 (through [S39a]) are themselves rooted in many-body physics and provide a common language between classical simulation methods and quantum circuit design.

The **quantitative finance** chapter develops the classical counterparts to the quantum finance applications in Section 6. Portfolio optimization, derivative pricing via Monte Carlo, and optimal trading strategies all have well-developed classical treatments that serve as the baseline against which quantum approaches must be measured.

The **probability, information, and risk** chapter connects to the information-theoretic foundations in Section 2 (particularly Witten [S17] and Watrous [S15]) and to the learning-theoretic questions in Section 5.

---


## Bibliography

### Overview

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

### Foundations

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

### Engineering

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
### Applications: Quantum Physics

| ID | Source | Notes |
|---|---|---|
| S26   | [2015 QCQFT](https://arxiv.org/abs/1503.08121)                                           | QCQFT investigates the intersection of quantum computing and quantum field theory by way of continuous variables. | 
| S27   | [2018 Simulating Quantum Fields  ](https://arxiv.org/abs/1811.10085)           | Considers the practical promises and challenges of Feynman's original vision    |
| S28   | [2018 QC Chemistry](https://arxiv.org/abs/1808.10402)           | Demonstrates how quantum algorithms can simulate molecular ground states more efficiently than classical methods, with applications to drug design.    |
| S29   | [2023 QC Many Body](https://arxiv.org/abs/2303.04850)           | Studies quantum algorithms for simulating many-body physics, focusing on fragmentation techniques to reduce circuit depth.                          |
| S30   | [2024 QC in High Energy](https://arxiv.org/abs/2307.03236)      | Investigates quantum computing approaches to lattice gauge theories and high-energy physics simulations, assessing resource requirements.             |
                   |

---

### Applications: Machine Learning

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

### Applications: Quantitative Finance

| ID | Source | Notes |
|---|---|---|
| S40   | [2018 QC Finance](https://arxiv.org/abs/1811.03975)                                              | Examines how quantum algorithms can accelerate option pricing and portfolio optimization, comparing performance to classical Monte Carlo methods. |
| S41   | [2018 QC Finance Monte Carlo](https://arxiv.org/abs/1805.00109)                                   | Demonstrates a quantum-accelerated Monte Carlo algorithm for computing risk measures in financial portfolios with provable quadratic speedups. |
| S42   | [2019 QC Finance](https://arxiv.org/abs/1807.03890)                                              | Surveys emerging quantum computing applications in finance, including credit scoring, derivative pricing, and fraud detection.               |
| S43   | [2020 Optimal Trading Quantum Annealing](https://arxiv.org/abs/1508.06182)                       | Proposes a quantum annealing framework for constructing optimal trading strategies under transaction-cost constraints.     

