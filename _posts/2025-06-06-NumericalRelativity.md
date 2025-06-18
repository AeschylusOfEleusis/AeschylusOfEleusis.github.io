---
layout:   post
title: "Numerical Relativity"
date: 2025-06-07 10:00:00 +0800
categories: [Numerical Relativity]
tags: [Numerical Relativity, Quantum Field Theory, Black holes, Worm holes, Scientific Computing]
math:       true        # enable KaTeX
---
# Notes on Numerical Relativity (Draft)

## Abstract

The following notes are an idiosyncratic sampling from the literature of numerical relativity. Focus is given to foundational materials in numerical relativity, gravitational collapse, and the problem of tracking horizons.    

**To be continued ...**

### 1. Finite Difference Approximation

| ID  | Link  | Notes |
| --- | ----- | ----- |
| S1  | [Richardson “Finite Differences” 1910](https://royalsocietypublishing.org/doi/10.1098/rsta.1911.0009) | Introduces early finite-difference approximations for solving differential equations and analyzes their stability and convergence properties. |
| S2  | [Dewitt “Early Days of Lagrangian Hydrodynamics” 1952](https://wwwrel.ph.utexas.edu/Members/dewitt/pubsBryce.pdf) | Reviews the historical development and foundational concepts of Lagrangian hydrodynamics up to the early 1950s. |
| S3  | [Dewitt “A numerical method for Lagrangian Hydrodynamics” 1953](https://wwwrel.ph.utexas.edu/Members/dewitt/pubsBryce.pdf) | Proposes a specific computational algorithm for solving fluid flow problems using a Lagrangian frame. |
| S4  | [Kreiss and Oliger “Comparison of methods for hyperbolic equations” 1972](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.2153-3490.1972.tb01547.x) | Compares the accuracy and efficiency of several finite-difference schemes applied to hyperbolic partial differential equations. |
| S5  | [Kreiss “Methods for approximate solution of time dependent problems” 1973](https://www.semanticscholar.org/paper/Methods-for-the-approximate-solution-of-time-Kreiss/283319b5fd1f578b66d40db8e26fa9f587bbd396) | Surveys techniques for discretizing and numerically integrating time-dependent PDEs with emphasis on stability criteria. |
| S6  | [Abarbanel et al “Difference schemes with fourth order accuracy for hyperbolic systems” 1975](https://epubs.siam.org/doi/abs/10.1137/0129029?journalCode=smjmap) | Develops and analyzes fourth-order accurate finite-difference schemes tailored for hyperbolic systems of equations. |
| S8  | [Berger and Oliger “Adaptive Mesh Refinement for Hyperbolic Equations” 1984](https://www.sciencedirect.com/science/article/abs/pii/0021999184900731) | Introduces the AMR algorithm that dynamically refines the computational grid based on solution features. |
| S9  | [Berger and Colella “Local Adaptive Mesh Refinement” 1989](https://www.sciencedirect.com/science/article/pii/0021999189900351) | Extends AMR techniques with block-structured grids to improve efficiency in multidimensional simulations. |


### 2. Foundations, Formalisms, and Toolkits

| ID  | Link  | Notes |
| --- | ----- | ----- |
| S10  | [Smarr et al “Collision of Two Black Holes” 1976](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.14.2443) | Presents one of the first numerical simulations of two black holes colliding, highlighting gravitational wave emission. |
| S11 | [Baumgarte and Shapiro “Numerical Relativity” 2010](https://bh0.physics.ubc.ca/Doc/baumgarte_shapiro/baumgarate_shapiro.pdf) | Offers a textbook-style introduction to numerical methods and formulations used in solving Einstein’s equations. |
| S12 | [Löffler et al “The Einstein Toolkit” 2011](https://arxiv.org/abs/1111.3344) | Describes an open-source, community-driven software infrastructure for relativistic astrophysics simulations. |
| S13 | [Clough et al “GRChombo: Numerical Relativity with Adaptive Mesh Refinement” 2015](https://arxiv.org/abs/1503.03436) | Introduces the GRChombo code enabling large-scale relativity simulations with dynamic mesh refinement. |
| S14 | [Choptuik et al “Probing Strong Field Gravity” 2015](https://arxiv.org/abs/1502.06853) | Explores methods and results for investigating strong-field gravitational dynamics via high-resolution numerics. |
| S15 | [Shibata “Numerical Relativity” 2016](https://www.worldscientific.com/worldscibooks/10.1142/9692?srsltid=AfmBOoqjEVlvLcbrWhfAKKxbYCf6aXEOvYGCio7urp9WKh2FsH6I-uQz#t=aboutBook) | Provides an authoritative overview of modern numerical relativity techniques in a graduate-level text. |
| S16 | [Scheel and Thorne “Nonlinear dynamics of curved spacetime” 2017](https://arxiv.org/abs/1706.09078) | Reviews advances in simulating highly nonlinear gravitational interactions, including binary black-hole mergers. |
| S17 | [Varma “Black Hole Simulations: From Supercomputers to Your Laptop” 2019](https://thesis.library.caltech.edu/11544/) | Demonstrates optimized algorithms that enable black-hole simulations on consumer-grade hardware. |
| S18 | [Gorard “Cauchy Problem in General Relativity via Wolfram Model” 2021](https://arxiv.org/abs/2102.09363) | Applies the Wolfram physics framework to formulate and solve the Cauchy problem in general relativity. |

### 3. Applications: Gravitational Collapse

| ID  | Link  | Notes |
| --- | ----- | ----- |
| S19 | [Choptuik “Universality and scaling in gravitational collapse of a massless scalar field” 1993](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.70.9) | Discovers critical phenomena—universality and power-law scaling—in scalar field gravitational collapse. |
| S20 | [Pretorius and Choptuik “Gravitational collapse in 2+1” 2000](https://arxiv.org/abs/gr-qc/0007008) | Investigates critical collapse phenomena in a (2+1)-dimensional spacetime via numerical evolution. |
| S21 | [Gundlach and Martin-Garcia “Critical phenomena in gravitational collapse” 2007](https://arxiv.org/abs/0711.4620) | Surveys analytic and numeric results on critical behavior during gravitational collapse across different matter models. |
| S22 | [Jałmużna et al “Scalar field critical collapse in 2+1” 2015](https://arxiv.org/abs/1510.02592) | Extends critical collapse studies of scalar fields to (2+1) dimensions with higher-resolution simulations. |
| S23 | [Figueras et al “Gregory Laflamme instability” 2020](https://arxiv.org/abs/2210.13501) | Studies the nonlinear evolution of the Gregory–Laflamme instability in higher-dimensional gravity. |

### 4. Applications: Horizon tracking 

| ID  | Link  | Notes |
| --- | ----- | ----- |
| S24 | [Libson et al “Event Horizons in Numerical Relavitity I” 1994](https://arxiv.org/abs/gr-qc/9412068) | Describes algorithms for locating event horizons in evolving spacetimes within numerical relativity codes. |
| S25 | [Masso et al “Event Horizons in Numerical Relativity II” 1998](https://arxiv.org/abs/gr-qc/9804059) | Refines and benchmarks horizon-finding methods against known analytic solutions to improve robustness. |
| S26 | [Thornburg “Event and Apparent Horizon Finders for Numerical Relativity” 2005](https://arxiv.org/abs/gr-qc/0512169) | Provides a comprehensive review of algorithms for detecting both event and apparent horizons in simulations. |
| S27 | [Cohen et al “Revisiting Event Horizon Finders” 2008](https://arxiv.org/abs/0809.2628) | Reassesses existing horizon-finding techniques and proposes improvements in accuracy and computational cost. |
| S28 | [Bohn et al “A Parallel Adaptive Event Horizon Finder” 2016](https://arxiv.org/abs/1606.00437) | Presents a scalable, parallel algorithm for tracking event horizons in three-dimensional simulations. |
| S29 | [Bohn et al “Toroidal Horizons” 2016](https://arxiv.org/abs/1606.00436) | Investigates the formation and properties of toroidal (doughnut-shaped) event horizons in dynamical spacetimes. |

---