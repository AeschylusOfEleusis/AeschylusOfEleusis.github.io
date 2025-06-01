---
layout:   post
title: "Option Trading"
date: 2025-05-31 10:00:00 +0800
categories: [Computational Finance]
tags: [Probability Information Risk, Quantum Field Theory, Path Integrals, Machine Learning, Computational Finance]
math:       true        # enable KaTeX
---
# Notes on Option Trading (Draft)

## Abstract
Materials concerning option trading are provided with brief notes. The sources navigate foundations, model building, asset classes, computational implementation and practice. An interdisciplinary perspective is assumed at the level of graduate students and researchers / practitioners in applied mathematics / theoretical physics. 

### 1 **Quantitative finance (theory to practice)**



| ID | Link | Notes |
|----|------|-------|
| S13 | [Joshi *Concepts & Practice of Mathematical Finance* 2008](https://www.cambridge.org/us/universitypress/subjects/mathematics/mathematical-finance/concepts-and-practice-mathematical-finance-2nd-edition?format=HB&isbn=9780521514088) | Pedagogical introduction bridging stochastic calculus and coding. |
| S22 | [Joshi *More Mathematical Finance* 2011](https://www.amazon.com/More-Mathematical-Finance-Suresh-Joshi/dp/0987122800) | Companion volume with further drills and implementation tips. |
| S7  | [Wilmott *Best of Wilmott Vol&nbsp;1* 2004](https://www.wiley.com/en-sg/The+Best+of+Wilmott+1%3A+Incorporating+the+Quantitative+Finance+Review-p-9780470023518) | Curated papers offering historical context and diverse perspectives. |
| S8  | [Wilmott *Best of Wilmott Vol&nbsp;2* 2005](https://www.wiley.com/en-us/The+Best+of+Wilmott+2-p-9780470031452) | Further model development and market microstructure. |
| S17 | [Wilmott *FAQ in Quantitative Finance* 2009](https://www.wiley.com/en-us/Frequently+Asked+Questions+in+Quantitative+Finance%2C+2nd+Edition-p-9780470685143) | Rapid reference for theoretical, numerical, and real-world questions. |


---


### 2 **Volatility surface & stochastic volatility (model development)**

| ID | Link | Notes |
|----|------|-------|
| S5 | [Lipton *Mathematical Methods for Foreign-Exchange* 2003](https://www.worldscientific.com/doi/epdf/10.1142/4694) | Closed-form solutions and calibrated SV jump-diffusions for financial engineering of FX options. |
| S6 | [Rebonato *Volatility and Correlation* 2004](https://www.wiley.com/en-us/Volatility+and+Correlation%3A+The+Perfect+Hedger+and+the+Fox%2C+2nd+Edition-p-9780470091401) | Empirical smile dynamics and correlation risk. Multi-asset hedging in stochastic-vol frameworks. |
| S10 | [Gatheral *The Volatility Surface* 2006](https://www.wiley.com/en-us/The+Volatility+Surface%3A+A+Practitioner's+Guide-p-9780471792512) | SVI/SVJ parameterisations and data-driven construction of arbitrage-free surfaces. |
| S26 | [Guyon & Henry-Labordère *Nonlinear Option Pricing* 2014](https://www.taylorfrancis.com/books/mono/10.1201/b16332/nonlinear-option-pricing-julien-guyon-pierre-henry-labordere) | Dupire PDEs forlocal stochastic volatility and calibration via optimal transport. |
| S31 | [Henry-Labordère *Model-Free Hedging* 2017](https://www.taylorfrancis.com/books/mono/10.1201/9781315161747/model-free-hedging-pierre-henry-labordere) | Martingale optimal-transport for robust bounds and hedges without committing to a specific SV model. |
| S33 | [Bayer et al. “Vol Surface Calibration” 2019](https://arxiv.org/abs/1908.08806) | Adjoint methods and deep learning for scalable volatility-surface calibration. |

---

### 3 **Interest-rates & fixed-income** 

| ID | Link | Notes |
|----|------|-------|
| S9  | [Brigo & Mercurio *Interest-Rate Models — Theory and Practice* 2006](https://link.springer.com/book/10.1007/978-3-540-34604-3) |  LIBOR-market, HJM, and BGM frameworks with implementation details. |
| S16 | [Rebonato, McKay, & White *LMM-SABR* 2009](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119206392) | Extends SABR dynamics for LMM producing smile-consistent swaption valuation. |

---

### 4 **Geometric & field theory approaches**

| ID | Link | Notes |
|----|------|-------|
| S11 | [Avramidi “Analytic & Geometric Methods for Heat Kernel Applications in Finance” 2007](https://www.researchgate.net/profile/Ivan-Avramidi/publication/255565392_Analytic_and_geometric_methods_for_heat_kernel_applications_in_finance/links/0c96053bc592b5a15e000000/Analytic-and-geometric-methods-for-heat-kernel-applications-in-finance.pdf) | Heat-kernel asymptotics for short-time implied-vol expansions. |
| S14 | [Henry-Labordère *Analysis, Geometry & Modeling in Finance* 2009](https://www.taylorfrancis.com/books/mono/10.1201/9781420087000/analysis-geometry-modeling-finance-pierre-henry-labordere) | Differential geometry, Malliavin calculus, and exotic option Greeks using geometric resourcs common to theoretical physics. |
| S15 | [Vazqueza and Faranelli “Geometry of Arbitrage” 2009](https://arxiv.org/abs/0908.3043) | Recasts no-arbitrage conditions as curvature constraints on fibre bundles. Translates finance into gauge-theoretic language. |
| S18 | [Taylor *Heat-Kernel Dissertation* 2010](https://d-nb.info/104960718X/34) | Doctoral work detailing symbolic computation of heat-kernel coefficients with direct option-pricing applications. |
| S19 | [Bourgade & Croissant “Heat-Kernel Expansions” 2010](https://arxiv.org/abs/cs/0511024) | Algorithmic recursion for coefficients employed in asymptotic implied-vol formulas. |
| S20 | [Vaccaro “Heat-Kernel Methods in Finance” 2010](https://arxiv.org/abs/1201.1437) | Review consolidates heat-kernel methods for jump-diffusion and stochastic-vol settings. |
| S24 | [Nastastiuk “Nelsonian Stochastics in Finance” 2013](https://arxiv.org/abs/1312.3247) | Extends Nelson’s stochastic mechanics to derivative pricing, drawing explicit analogies with quantum potential. |
| S29 | [Kleinert & Korbel “Lévy Paths & Option Pricing” 2015](https://arxiv.org/abs/1503.05655) | Path-integral methods to price under Lévy processes, paralleling quantum mechanics in fractional dimension. |
| S28 | [Avramidi *Heat Kernel Methods* 2015](https://link.springer.com/book/10.1007/978-3-319-26266-6) | Comprehensive monograph on geometric asymptotics, spectral theory and financial short-maturity asymptotics. |
| S32 | [Baaquie *Quantum Field Theory in Economics & Finance* 2018](https://www.cambridge.org/us/universitypress/subjects/physics/econophysics-and-financial-physics/quantum-field-theory-economics-and-finance?format=HB&isbn=9781108423151) | Introduces QFT path-integral methods for term-structure and equity-option models. |
| S36 | [Faranelli “Geometric Arbitrage” 2021](https://arxiv.org/abs/0910.1671) | Revisits arbitrage-free pricing via symplectic geometry. Coordinate-free hedging strategies. |
| S37 | [Faranelli & Takada “Quantum Arbitrage” 2021](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3404437) | Proposes a quantum framework for arbitrage detection. Potential quantum-computational pay offs. |

---

### 5 Numerical methods and computational implementation 

| ID | Link | Notes |
|----|------|-------|
| S3  | [Glasserman *Monte Carlo Methods in Financial Engineering* 2000](https://link.springer.com/book/10.1007/978-0-387-21617-1) | Canonical text defining variance-reduction and path-generation techniques. |
| S4  | [Jaeckel *Monte Carlo Methods in Finance* 2001](https://www.wiley.com/en-us/Monte+Carlo+Methods+in+Finance-p-9780471497417) | Quasi-random sequences and Greeks estimation for high-precision pricing. |
| S12 | [Joshi *C++ Design Patterns and Derivatives Pricing* 2008](https://www.cambridge.org/us/universitypress/subjects/mathematics/mathematical-finance/c-design-patterns-and-derivatives-pricing-2nd-edition?format=PB&isbn=9780521721622) | Maps C++ patterns to scalable pricing engines. |
| S23 | [Hirsa *Computational Methods in Finance* 2016](https://www.taylorfrancis.com/books/mono/10.1201/b12755/computational-methods-finance-ali-hirsa) | Surveys finite-difference, tree, Fourier, and Monte-Carlo. |
| S27 | [Hilpisch *Python for Finance* 2014](https://www.oreilly.com/library/view/python-for-finance/9781492024323/) | Demonstrates NumPy/SciPy-based option pricers for rapid prototyping. |
| S30 | [Hilpisch *Python for Derivatives Analytics* 2015](https://www.oreilly.com/library/view/derivatives-analytics-with/9781119037996/) | Vectorised Greeks, calibration, and risk dashboards in pandas. |
| S35 | [Ballabio *Implementing QuantLib* 2020](https://www.implementingquantlib.com) | Guide to the industry-standard QuantLib open-source library. |

---

### 6 Trading, hedging & risk management in practice

| ID | Link | Notes |
|----|------|-------|
| S1  | [Natenberg *Option Volatility & Pricing* 1994](https://www.mheducation.com/highered/mhp/product/option-volatility-pricing-advanced-trading-strategies-techniques.html) | Classic trader’s guide translating Greeks into real-world spread and skew trades. |
| S2  | [Taleb *Dynamic Hedging* 1996](https://www.wiley.com/en-cn/Dynamic+Hedging%3A+Managing+Vanilla+and+Exotic+Options-p-9780471152804) | Path-wise hedging and “local-delta-gamma” approach. |
| S21 | [Sinclair *Option Trading* 2010](https://www.wiley.com/en-us/Option+Trading%3A+Pricing+and+Volatility+Strategies+and+Techniques-p-9780470642528) | Blends practitioner intuition with quantitative models. |
| S25 | [Sinclair *Volatility Trading* (2e)2013 ](https://www.wiley.com/en-us/Volatility+Trading%2C+%2B+Website%2C+2nd+Edition-p-9781118416723) | Variance swaps, VIX products, and vol-arbitrage trades. |
| S34 | [Sinclair *Positional Option Trading* 2020](https://www.wiley.com/en-us/Positional+Option+Trading%3A+An+Advanced+Guide-p-9781119583530) | Regime-based positional strategies. |
| S38 | [Taleb “Fat Tails & Nonlinear Exposure” 2022](https://arxiv.org/abs/2001.10488) | Antifragile payoff design under power-law tails and 'black swans'. |