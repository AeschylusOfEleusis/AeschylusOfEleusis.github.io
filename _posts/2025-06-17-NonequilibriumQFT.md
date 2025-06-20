---
layout:   post
title: "Nonequilibrium Quantum Field Theory"
date: 2025-06-17 10:00:00 +0800
categories: [Quantum Field Theory]
tags: [Machine Learning,Stochastic Calculus, Fractional Calculus, Scientific Computing, Quantum Computing, Stochastic Quantization, NonequilibriumQFT,Quantum Field Theory]
math:       true        # enable KaTeX
---
# Notes on Nonequilibrium Quantum Field Theory  (Draft)

## Abstract
Sources in nonequilibrium quantum field theory are provided following foundational materials in equilibrium statistical mechanics. The philosophy of Euclidean field theory is assumed: Flucutations of either quantum or thermal (statistical) physical orgin are viewed as mathematically equivalent. Physical applications include fields at finite temperature; e.g., Bose-Einstein condensation, relativistic heavy ion collisions, and cosmology of the early universe.  

**To be continued ...**

## 1. Statistical Mechanics

| ID  | Link | Notes |
|-----|------|-------|
| S1 | [Jaynes *”Information Theory and Statistical Mechanics”* 1957](https://journals.aps.org/pr/abstract/10.1103/PhysRev.106.620) | Foundational paper linking statistical mechanics with Bayesian information theory. |
| S2 | [Huang *”Statistical Mechanics”* 1987](https://www.wiley.com/en-us/Statistical+Mechanics%2C+2nd+Edition-p-9780471815181) | Comprehensive graduate-level textbook on equilibrium statistical mechanics. |
| S3 | [Wheeler *”Statistical Mechanics: Preface”* 2005](https://www.reed.edu/physics/faculty/wheeler/documents/Thermo%20&%20Statistical%20Mechanics/Class%20Notes/A.%20Preface.pdf) | Introductory overview outlining the philosophy and scope of Wheeler's statistical mechanics course. |
| S4 | [Wheeler *”Statistical Mechanics: Chapter 1”* 2005](https://www.reed.edu/physics/faculty/wheeler/documents/Thermo%20&%20Statistical%20Mechanics/Class%20Notes/Chapter%201.pdf) | First chapter introducing the basic postulates and microscopic foundations of statistical mechanics. |
| S5 | [Wheeler *”Statistical Mechanics: Chapter 2”* 2005](https://www.reed.edu/physics/faculty/wheeler/documents/Thermo%20&%20Statistical%20Mechanics/Class%20Notes/Chapter%202.pdf) | Discusses ensembles, particularly the microcanonical and canonical ensembles. |
| S6 | [Wheeler *”Statistical Mechanics: Chapter 3”* 2005](https://www.reed.edu/physics/faculty/wheeler/documents/Thermo%20&%20Statistical%20Mechanics/Class%20Notes/Chapter%203.pdf) | Explores statistical mechanics applications in thermodynamic equilibrium. |
| S7 | [Sethna *”Entropy, Order Parameters, and Complexity”* 2024](https://sethna.lassp.cornell.edu/StatMech/EntropyOrderParametersComplexity20.pdf) | Modern text bridging concepts in thermodynamics, information theory, and complexity. |

## 2. Nonequilibrium Statistical Physics

| ID  | Link | Notes |
|-----|------|-------|
| S8  | [Wetterich *”Time Evolution of Non-Equilibrium Effective Action”* 1996](https://arxiv.org/abs/hep-th/9612206) | Introduces an effective action formalism for describing nonequilibrium time evolution. |
| S9  | [Reichl *”A Modern Course in Statistical Physics”* 2016](https://www.wiley.com/en-us/A+Modern+Course+in+Statistical+Physics%2C+4th+Edition-p-9783527413492) | Advanced textbook combining equilibrium and nonequilibrium statistical mechanics. |
| S10 | [Zwanzig *”Nonequilibrium Statistical Mechanics”* 2001](https://global.oup.com/academic/product/nonequilibrium-statistical-mechanics-9780195140187?cc=us&lang=en) | Clear exposition of projection operator methods in nonequilibrium systems. |
| S11 | [Ebeling and Sokolov *”Thermodynamics and Stochastics of Nonequilibrium Systems”* 2006](https://www.worldscientific.com/worldscibooks/10.1142/2012?srsltid=AfmBOoojok4ZccRGIm-o_xLbPlkMim6C_uC4nX7xBGMYabnjzrlNkbuK#t=aboutBook) | Focuses on stochastic processes and their thermodynamic interpretation in nonequilibrium systems. |
| S12 | [Le Bellac *”Nonequilibrium Statistical Mechanics”* 2007](https://cel.hal.science/cel-00176063) | Lecture notes on kinetic theory and stochastic processes for non-equilibrium phenomena. |
| S13 | [Graf *”Non-Equilibrium Statistical Mechanics”* 2011](https://edu.itp.phys.ethz.ch/hs11/nesm/NESMLN.pdf) | ETH Zurich lecture notes providing a mathematically rigorous treatment of nonequilibrium physics. |
| S14 | [Pavliotis *”Non-Equilibrium Statistical Mechanics”* 2012](https://www.ma.ic.ac.uk/~pavl/noneqstatmech.pdf) | Lecture notes emphasizing stochastic processes and coarse-graining in nonequilibrium systems. |
| S15 | [Pruessner *”Non-Equilibrium Statistical Mechanics”* 2016](https://www.ma.imperial.ac.uk/~pruess/publications/noneq.pdf) | Reviews critical phenomena and self-organized criticality in nonequilibrium systems. |
| S16 | [Livi and Politi *”Nonequilibrium Statistical Physics”* 2017](https://www.cambridge.org/core/books/nonequilibrium-statistical-physics/FD152FD18FC04BA5B4505F2D85E070C1#fndtn-information) | Comprehensive book exploring chaotic dynamics and thermodynamic fluctuations. |
| S17 | [Tong *”Statistical Field Theory”* 2017](https://www.damtp.cam.ac.uk/user/tong/sft.html) | Lecture notes introducing field-theoretic techniques for both equilibrium and nonequilibrium systems. |
| S18 | [Arovas *”Lecture Notes on Nonequilibrium Statistical Physics”* 2018](https://courses.physics.ucsd.edu/2013/Fall/physics210b/LECTURES/STOCHASTIC.pdf) | Covers stochastic processes, master equations, and fluctuation-dissipation relations. |
| S19 | [Orioli and Berges *”Fluctuation-Dissipation and Universal Transport”* 2019](https://arxiv.org/pdf/1810.12392) | Explores the emergence of universal transport in far-from-equilibrium systems. |
| S20 | [Berthier and Kurchan *”Lectures on Non-Equilibrium Active Systems”* 2019](https://arxiv.org/abs/1906.04039) | Lectures on active matter and nonequilibrium dynamics in soft condensed matter. |

## 3. Nonequilibrium Quantum Fields

| ID  | Link | Notes |
|-----|------|-------|
| S21 | [Wetterich *”Non-equilibrium Time Evolution in QFT”* 1997](https://arxiv.org/abs/hep-th/9703006) | Applies functional methods to model nonequilibrium dynamics in quantum field theory. |
| S22 | [Bettencourt and Wetterich *”Time Evolution in Non-Equilibrium Field Theories”* 1997](https://arxiv.org/abs/hep-ph/9712429) | Investigates time evolution and initial value problems in interacting field theories. |
| S23 | [Aarts et al *”Exact and Truncated Dynamics in Nonequilibrium Field Theory”* 2000](https://arxiv.org/abs/hep-ph/0007357) | Compares exact and approximate solutions in real-time nonequilibrium field theory. |
| S24 | [Berges *”Introduction to Nonequilibrium QFT”* 2004](https://arxiv.org/abs/hep-ph/0409233) | Review of nonequilibrium methods including the 2PI effective action and Boltzmann equations. |
| S25 | [Berges et al *”Prethermalization”* 2004](https://arxiv.org/abs/hep-ph/0403234) | Describes universal behavior in early-time dynamics of isolated quantum systems. |
| S26 | [Berges et al *”Nonperturbative Renormalization for 2PI Effective Action”* 2005](https://arxiv.org/abs/hep-ph/0503240) | Explores renormalization of the two-particle irreducible effective action in quantum fields. |
| S27 | [Kapusta *”Finite Temperature Field Theory”* 2006](https://www.cambridge.org/core/books/finitetemperature-field-theory/880F1E5BEB7E1DF7E516C9B1507EC4A4#fndtn-information) | Standard textbook covering thermal quantum field theory and real-time formalisms. |
| S28 | [Tauber *”Field Theory Approaches to Nonequilibrium Dynamics”* 2006](https://arxiv.org/abs/cond-mat/0511743) | Review article linking field theory and stochastic processes in statistical physics. |
| S29 | [Rammer *”QFT of Non-equilibrium States”* 2009](https://www.cambridge.org/core/books/quantum-field-theory-of-nonequilibrium-states/753A0F8533485FF98BB64D80AD4D7BD1#fndtn-information) | Treats quantum transport and Green’s functions in non-equilibrium condensed matter systems. |
| S30 | [Calzetta and Hu *”Nonequilibrium Quantum Field Theory”* 2009](https://www.cambridge.org/core/books/nonequilibrium-quantum-field-theory/335367EAFE8072499CF7DA85AAAACAAE#fndtn-information) | A foundational text on quantum field dynamics in cosmology and many-body systems. |
| S31 | [Berges *”Nonequilibrium Quantum Fields: From Cold Atoms to Cosmology”* 2015](https://arxiv.org/abs/1503.02907) | Surveys applications of nonequilibrium QFT from laboratory systems to early-universe physics. |
| S32 | [Glavan and Prokopec *”Introduction to Non-Equilibrium QFT”* 2017](https://webspace.science.uu.nl/~proko101/LecturenotesNonEquilQFT.pdf) | Lecture notes introducing Keldysh formalism and real-time techniques for quantum fields. |
| S33 | [Berges et al *”Entanglement and Thermalization”* 2018](https://arxiv.org/abs/1812.08120) | Discusses the role of quantum entanglement in thermalization of closed quantum systems. |