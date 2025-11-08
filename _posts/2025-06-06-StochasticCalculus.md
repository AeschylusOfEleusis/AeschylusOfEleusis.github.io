---
layout:   post
title: "Stochastic Calculus"
date: 2025-06-07 10:00:00 +0800
categories: [Computational Finance]
tags: [Stochastic Quantization, Quantum Field Theory, Numerical Relativity, Option Trading, Scientific Computing, Worm holes, Probability Information Risk]
math:       true        # enable KaTeX
---
# Notes on Stochastic Calculus (Draft)

## Abstract
Notes on stochastic calculus are provided. The first section views Brownian motion using Langevin equations (conventional to physics literature); along with stochastic differential equations (conventional to mathematics literature). Following sections generalize to: 1. Brownian motion on curved manifolds, 2. Nelson's stochastic mechanics, 3. Relativistic diffusion, and 4. Stochastic partial differential equations. Detailed numerical methods for computational implementation are included throughout the notes. 
    
**To be continued ...**


## 1. Brownian Motion and Stochastic Differential Equations

| ID  | Link                                                                                                                                                                            | Notes                                                                                                       |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| S1  | [Chandrasekhar “Brownian Motion” 1943](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.15.1)                                                                            | Presents a classic, comprehensive review of the physical theory and mathematical description of Brownian motion. |
| S2  | [Anderson “Reverse time diffusion” 1982](https://www.sciencedirect.com/science/article/pii/0304414982900515)                                                                       | Investigates the mathematical properties of diffusion processes when considered backward in time.           |
| S3  | [Karatzas and Shreve “Stochastic Calculus” 1998](https://link.springer.com/book/10.1007/978-1-4612-0949-2)                                                                         | Provides a rigorous, graduate-level treatment of Itô calculus and its applications to SDEs.                 |
| S4  | [Arnold “Langevin equations” 1999](https://arxiv.org/pdf/hep-ph/9912208)                                                                                                         | Surveys the derivation and applications of Langevin equations in physics.                                   |
| S5  | [Arnold “Symmetric path integrals” 1999](https://arxiv.org/abs/hep-ph/9912209)                                                                                                   | Develops a symmetric formulation of path integrals for stochastic and quantum systems.                       |
| S6  | [Kloeden and Platen “Numerical solutions” 1999](https://link.springer.com/book/10.1007/978-3-662-12616-5)                                                                           | Introduces numerical algorithms for strong and weak approximations of stochastic differential equations.    |
| S7  | [Garcia-Palacios “Introduction to stochastic processes” 2007](https://arxiv.org/abs/cond-mat/0701242)                                                                                | Offers an accessible overview of key concepts in stochastic process theory, including Brownian motion.      |
| S8  | [Baine “Stochastic Calculus and commutation relations” 2010](https://www.sciencedirect.com/science/article/pii/S0304414910000256#:~:text=Abstract,equations%2C%20on%20the%20Fock%20space.) | Examines the interplay between stochastic calculus and operator commutation in Fock space.                   |
| S9  | [Dengler “Derivation of Langevin equations” 2015](https://arxiv.org/abs/1506.02650)                                                                                                | Derives Langevin dynamics from underlying microscopic Hamiltonian models.                                   |
| S10 | [Särkkä and Solin “Applied SDE” 2019](https://www.cambridge.org/core/books/applied-stochastic-differential-equations/6BB1B8B0819F8C12616E4A0C78C29EAA)                          | Covers practical methods for modeling time series with stochastic differential equations.                   |
| S11 | [Milstein and Tretyakov “Stochastic Numerics” 2021](https://link.springer.com/book/10.1007/978-3-662-10063-9)                                                                         | Presents advanced numerical schemes for simulating stochastic dynamical systems with error analysis.        |

---

## 2. Brownian Motion on Curved Manifolds

| ID  | Link                                                                                                                                                                                    | Notes                                                                                                    |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| S12 | [Itô “Brownian Motion in a Lie Group” 1950](https://projecteuclid.org/journals/proceedings-of-the-japan-academy/volume-26/issue-8/Brownian-motions-in-a-Lie-group/10.3792/pja/1195571633.full) | Introduces SDEs defining Brownian paths on Lie group manifolds.                                          |
| S13 | [Itô “Brownian Motion in a Differentiable Manifold Ia” 1950](https://projecteuclid.org/journals/nagoya-mathematical-journal/volume-1/issue-none/Stochastic-differential-equations-in-a-differentiable-manifold/nmj/1118764702.full) | Develops the foundational stochastic differential equations on differentiable manifolds.                 |
| S14 | [Itô “Brownian Motion in a Differentiable Manifold Ib” 1951](https://www.cambridge.org/core/journals/nagoya-mathematical-journal/article/on-a-formula-concerning-stochastic-differentials/CA39C46B3829C055DBD1BF839BA0E140) | Extends to explicit formulae for stochastic differentials in manifold coordinates.                        |
| S15 | [Itô “Brownian Motion in a Differentiable Manifold II” 1953](https://projecteuclid.org/journals/kyoto-journal-of-mathematics/volume-28/issue-1/Stochastic-Differential-Equations-in-a-Differentiable-Manifold-2/10.1215/kjm/1250777513.full) | Further generalizes manifold SDEs with curvature considerations.                                        |
| S16 | [Itô “The Brownian motion and tensor fields on Riemannian manifold” 1962](https://link.springer.com/chapter/10.1007/BFb0013327)                                                          | Examines interactions between Brownian motion and tensor fields on Riemannian spaces.                    |
| S17 | [Elworthy “Geometric Aspects of Diffusions on Manifolds” 1988](https://link.springer.com/chapter/10.1007/BFb0086183)                                                                   | Surveys geometric frameworks underpinning diffusion in manifold settings.                                |
| S18 | [Hsu “Brownian motion and Riemannian Geometry” 1988](https://sites.math.northwestern.edu/~ehsu/Brownian%20Motion%20and%20Riemannian%20Geometry.pdf)                                    | Links probabilistic Brownian analysis with Riemannian geometric structures.                              |
| S19 | [Kleinert and Shabanov “Brownian Motion in a space with curvature and torsion” 1995](https://arxiv.org/abs/cond-mat/9504121)                                                           | Analyzes Brownian paths in spaces endowed with both curvature and torsion.                               |
| S20 | [Hsu “Brownian motion on Riemannian Manifolds” 2000](https://people.math.harvard.edu/~ctm/home/text/class/harvard/219/21/html/home/sources/hsu.pdf)                                | Lecture notes constructing Brownian motion via the Laplace–Beltrami operator.                            |
| S21 | [Hsu “Stochastic Analysis on Manifolds” 2001](https://bookstore.ams.org/view?ProductCode=GSM/38)                                                                                    | Compiles advanced tools and theorems for SDEs on manifold domains.                                       |
| S22 | [Marjanovic “Numerical methods for SDE in Lie Groups” 2018](https://ieeexplore.ieee.org/abstract/document/8270577)                                                                   | Proposes structure-preserving integration schemes for Lie-group-valued stochastic differential equations. |
| S23 | [Chandra et al “Langevin dynamics for Yang-Mills” 2022](https://arxiv.org/abs/2006.04987)                                                                                            | Applies Langevin-based methods to simulate Yang–Mills gauge fields.                                       |
| S24 | [Muniz et al “Itô SDEs on Matrix Lie Groups” 2021](https://arxiv.org/abs/2102.04131)                                                                                                | Develops an Itô–SDE framework explicitly for processes valued in matrix Lie groups.                      |

---

## 3. Stochastic Mechanics

| ID  | Link                                                                                                                                                                                                 | Notes                                                                                                         |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| S25 | [Nelson “Stochastic Mechanics” 1966](https://journals.aps.org/pr/abstract/10.1103/PhysRev.150.1079)                                                                                                    | Introduces a stochastic-process approach to derive quantum dynamics from underlying Brownian trajectories.   |
| S26 | [Nelson “Dynamical Theories of Brownian Motion” 1967](https://press.princeton.edu/books/paperback/9780691079509/dynamical-theories-of-brownian-motion)                                              | Develops a unified theoretical framework relating Brownian motion to quantum mechanical equations.          |
| S27 | [Dohrn and Guerra “Stochastic Mechanics on Riemannian Manifolds” 1978](https://link.springer.com/article/10.1007/BF02804667)                                                                         | Extends Nelson’s formulation to curved spaces by incorporating Riemannian geometry into stochastic dynamics. |
| S28 | [Yasue “Stochastic Mechanics: A Review” 1979](https://link.springer.com/article/10.1007/BF00669566)                                                                                                   | Provides a comprehensive review of stochastic mechanics developments and their physical interpretations.      |
| S29 | [Dewitt-Morette et al “Stochastic scheme for Schrodinger equations” 1980](https://www.numdam.org/item/?id=AIHPA_1980__32_4_327_0)                                                                    | Introduces stochastic path‐integral techniques to solve Schrödinger-type equations.                            |
| S30 | [Gaveau et al “Relativistic stochastic mechanics” 1984](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.53.419)                                                                            | Proposes a Lorentz-invariant extension of Nelson’s stochastic mechanics.                                       |
| S31 | [Nelson “Quantum Fluctuations” 1985](https://web.math.princeton.edu/~nelson/books/qf.pdf)                                                                                                             | Explores stochastic interpretations of quantum field fluctuations.                                              |
| S32 | [Bacciagaluppi “Nelsonian Mechanics” 1998](https://arxiv.org/abs/quant-ph/9811040)                                                                                                                   | Reexamines philosophical foundations and consistency of Nelson’s stochastic mechanics.                         |
| S33 | [Bacciagaluppi “Conceptual Introduction to Nelson’s Mechanics” 2005](https://philsci-archive.pitt.edu/8853/)                                                                                         | Offers an accessible conceptual overview of the stochastic interpretation of quantum theory.                   |
| S34 | [Cresson “Stochastic embedding of dynamical systems” 2005](https://arxiv.org/abs/math/0509713)                                                                                                       | Introduces techniques to embed deterministic systems into stochastic frameworks for analysis.                  |
| S35 | [Derakhshani “Stochastic mechanics” 2018](https://arxiv.org/abs/1804.01394)                                                                                                                          | Surveys modern developments and generalizations of stochastic mechanics.                                       |
| S36 | [Kuipers “Analytic continuation of stochastic mechanics” 2022](https://arxiv.org/pdf/2109.10710)                                                                                                     | Explores analytic continuation methods within stochastic mechanics to connect to complex domains.              |
| S37 | [Kuipers “Stochastic mechanics and Brownian motion” 2023](https://arxiv.org/abs/2301.05467)                                                                                                          | Analyzes the foundational role of Brownian motion in contemporary stochastic mechanics approaches.             |

---

## 4. Relativistic Diffusion

| ID  | Link                                                                                                                                                                                    | Notes                                                                                       |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| S38 | [Jacobson and Schulman “Quantum Stochastics” 1984](https://iopscience.iop.org/article/10.1088/0305-4470/17/2/023)                                                                         | Develops an operator-based quantum description of stochastic processes.                      |
| S39 | [Jacobson “Random walk representation of spinors” 1985](https://pubs.aip.org/aip/jmp/article-abstract/26/7/1600/228178/Random-walk-representations-for-spinor-and-vector?redirectedFrom=fulltext) | Represents spinor fields via discrete random-walk models.                                   |
| S40 | [Polonyi “Path integral for Dirac equation I” 1998](https://arxiv.org/abs/hep-th/9809115)                                                                                              | Introduces a path-integral formulation for the free Dirac equation.                         |
| S41 | [Polonyi “Path integral for Dirac equation II” 1999](https://arxiv.org/abs/hep-th/9809116)                                                                                             | Extends the path-integral approach to interacting Dirac fields.                             |
| S42 | [Franchi “Relativistic Diffusion in the Godel Universe” 2007](https://arxiv.org/abs/math/0612020)                                                                                       | Studies diffusion processes in the rotating Gödel spacetime geometry.                      |
| S43 | [Dunkel and Hänggi “Relativistic Brownian Motion” 2008](https://arxiv.org/abs/0812.1996)                                                                                               | Provides a covariant theory of Brownian motion consistent with special relativity.         |
| S44 | [Kuipers “Stochastic mechanics on Lorentzian manifolds” 2021](https://arxiv.org/abs/2101.12552)                                                                                         | Develops stochastic mechanical models on Lorentzian manifold backgrounds.                  |

---

## 5. Stochastic Partial Differential Equations

| ID  | Link                                                                                                                                                                               | Notes                                                                                               |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| S45 | [Hochberg et al “Renormalization Group and Effective Action” 1998](https://arxiv.org/abs/hep-th/9809198)                                                                            | Applies renormalization group methods to compute effective actions in stochastic field theories.   |
| S46 | [Hochberg et al “Zeta functions and effective action” 1998](https://arxiv.org/abs/hep-th/9809206)                                                                                 | Uses zeta-function regularization to analyze effective actions for stochastic PDEs.                |
| S47 | [Hochberg et al “Stochastic Partial Differential Equations” 1999](https://arxiv.org/pdf/cond-mat/9904215)                                                                          | Provides a foundational renormalization treatment for stochastic partial differential equations.   |
| S48 | [Hochberg et al “Effective potential for SPDE”](https://arxiv.org/abs/cond-mat/9904207)                                                                                           | Derives the effective potential governing fluctuations in SPDEs.                                    |
| S49 | [Hochberg et al “Heat kernel for SPDE” 2000](https://arxiv.org/abs/cond-mat/0009424)                                                                                               | Develops heat-kernel techniques to solve stochastic PDEs.                                           |
| S50 | [Amaral and Roditi “Gaussian effective potential and SPDE” 2007](https://www.sciencedirect.com/science/article/abs/pii/S0378437107007224)                                            | Studies Gaussian effective potential methods applied to SPDEs.                                      |
| S51 | [Tauber “Field Theoretic Methods” 2007](https://arxiv.org/abs/0707.0794)                                                                                                          | Reviews field-theoretic approaches to critical dynamics in stochastic systems.                     |
| S52 | [Schehr et al “Stochastic Processes and Random Matrices” 2015](https://academic.oup.com/book/43715)                                                                                  | Explores connections between stochastic growth models and random matrix theory.                            |
| S53 | [Chow “Stochastic Partial Differential Equations” 2015](https://www.routledge.com/Stochastic-Partial-Differential-Equations/Chow/p/book/9781466579552)                             | Presents a comprehensive textbook on both theory and applications of SPDEs.                         |
| S54 | [Ovchinnikov “Supersymmetry of stochastics” 2015](https://arxiv.org/abs/1511.03393)                                                                                                | Explores supersymmetric structures emerging in stochastic differential equations.                   |
| S55 | [Zhang and Karniadakis “Numerical methods for SPDE” 2017](https://link.springer.com/book/10.1007/978-3-319-57511-7)                                                                 | Surveys computational schemes for accurately simulating stochastic partial differential equations. |

## Appendix: 11.7.2025

Quantum mechanics admits several representations whose interconnections are often opaque. Parisi–Wu stochastic quantization introduces a computational time evolution toward a Euclidean quantum measure; while Onsager–Machlup (OM) / MSRJD formalisms express stochastic dynamics as path integrals over trajectories. By comparison, Nelson's stochastic mechanics interprets quantum motion as an underlying diffusion in real time; with the de Broglie–Bohm view yielding deterministic trajectories guided by a pilot wave. In the following note, these approaches are demonstrated as different limits of the same stochastic–variational structure.

### Parisi–Wu

Consider Euclidean quantum mechanics with coordinate \(x(\tau)\) and action
$$
S_E[x] = \int_0^T ds\,
\Big[\tfrac{1}{2}\dot x^2 + V(x)\Big].
$$

Parisi and Wu introduce a fictitious time \(s\) with stochastic partial differential equation
$$
\partial_\tau x(\tau,s)
= -\frac{\delta S_E}{\delta x(\tau,s)} + \eta(\tau,s),
$$
where \(\eta\) is Gaussian white noise with
$$
\langle\eta(\tau,s)\eta(\tau',s')\rangle
  = 2\,\delta(\tau-\tau')\delta(s-s').
$$
The Fokker–Planck equation for the functional probability \(P[x;s]\) is
$$
\partial_s P[x;s]
= \int d\tau\,\frac{\delta}{\delta x(\tau)}
  \left(\frac{\delta}{\delta x(\tau)}+ \frac{\delta S_E}{\delta x(\tau)}\right)P,
$$
with stationary solution \(P_{\mathrm{eq}}[x]\propto e^{-S_E[x]}\).
The \(s\to\infty\) limit reproduces the Euclidean path integral of quantum mechanics.

### Onsager–Machlup / MSRJD

The Parisi and Wu equation is of the form
\(\partial_s x = F[x] + \eta\),
with \(F[x] = \ddot x - V'(x)\).
Let \(\tilde{x}(\tau,s)\) be a response field.
The MSRJD functional integral is
$$
Z = \int \mathcal{D}\!\left[x, \tilde{x}\right] e^{S_{M}[x,\tilde{x}]}
$$
with
$$
S_{M}[x,\tilde{x}]
= \int ds\,d\tau
\left[
  i\tilde x(\partial_s x - \ddot x + V'(x))
  - \tilde x^2
\right].
$$
Integrating over \(\tilde x\) yields the Onsager–Machlup action
$$
S_{O}[x]
= \tfrac{1}{4}\!\int\! ds\,d\tau
  \big(\partial_s x - \ddot x + V'(x)\big)^2
- \tfrac{1}{2}\!\int\! ds\,d\tau\,V''(x).
$$
The most probable path satisfies
\(\partial_s x = \ddot x - V'(x)\),
the deterministic Parisi–Wu relaxation.
As \(s\!\to\!\infty\), the system approaches the equilibrium measure \(e^{-S_E[x]}\).

### Nelson's Stochastic Mechanics

Nelson's stochastic mechanics describes a physical diffusion process in real time \(t\),
$$
dx_t = b_\pm(x_t,t)\,dt + \sqrt{2\nu}\,dW_t^\pm,
\qquad
\nu=\frac{\hbar}{2m},
$$
with forward/backward drifts \(b_\pm = v \pm u\), where
$$
v = \frac{b_+ + b_-}{2} = \frac{1}{m}\nabla S,
\quad
u = \frac{b_+ - b_-}{2} = \nu\nabla\ln\rho.
$$
The symmetric Onsager–Machlup functional for this double diffusion is
$$
S_N[x]
= \frac{1}{4\nu}\int dt\,
  \Big[(\dot x - v)^2 + u^2\Big]
  + \frac{1}{2}\int dt\,\nabla\!\cdot v.
$$
Varying \(S_N\) yields Nelson's stochastic Newton law
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v
   - (u\!\cdot\!\nabla)u
   - \nu\nabla^2 u\big)
= -\nabla V,
$$
which, using \(u=\nu\nabla\ln\rho\), reduces to
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v\big)
= -\nabla(V+Q),
\quad
Q = -\frac{\hbar^2}{2m}\,
    \frac{\nabla^2\sqrt\rho}{\sqrt\rho}.
$$
These results are are equivalent to the Schrödinger equation under
\(\psi=\sqrt\rho\,e^{iS/\hbar}\).

### de Broglie–Bohm

The de Broglie–Bohm (dBB) theory prescribes deterministic trajectories
$$
\dot x = \frac{1}{m} \nabla S,
$$
where \(S\) satisfies the quantum Hamilton–Jacobi equation
$$
\partial_t S + \frac{(\nabla S)^2}{2m} + V + Q = 0.
$$
In the OM/MSRJD representation, the dBB trajectories correspond to extremals of the functional: either the deterministic limit of the Nelson process or the \(s\!\to\!\infty\) stationary flow of the Parisi–Wu process.

### Conclusion

The Onsager–Machlup / MSRJD formalism provides a single variational language:

1. **Computational time diffusion (Parisi–Wu):** a gradient flow in functional space whose equilibrium measure is \(e^{-S_E}\) with computational diffusion converging to the quantum ensemble,
2. **Real time diffusion (Nelson):** a symmetric stochastic process with equilibrium \(\rho=|\psi|^2\) with real diffusion of stochastic fluctuations around the quantum flow,
3. **Deterministic flow (Bohm):** the extremal trajectories of the same action, obtained when the stochastic term vanishes, yielding deterministic limit mean current lines of the same ensemble.

The quantum potential appears universally as the curvature term generated by the divergence of the drift in the Onsager–Machlup functional.

Applying the Onsager–Machlup / MSRJD method to Parisi–Wu stochastic quantization produces a diffusion in fictitious time \(s\) whose stationary state reproduces quantum mechanics. Applying the same formalism to Nelson's stochastic mechanics yields the physical diffusion equations that reproduce the Schrödinger dynamics. In the deterministic limit, the Onsager–Machlup extremals coincide with de Broglie–Bohm pilot-wave trajectories. In short, stochastic quantization, stochastic mechanics, and the pilot-wave theory are successive reductions of a single stochastic–variational framework defined by the Onsager–Machlup action.: 

Quantum mechanics admits several representations whose interconnections are often opaque. Parisi–Wu stochastic quantization introduces a computational time evolution toward a Euclidean quantum measure; while Onsager–Machlup (OM) / MSRJD formalisms express stochastic dynamics as path integrals over trajectories. By comparison, Nelson's stochastic mechanics interprets quantum motion as an underlying diffusion in real time; with the de Broglie–Bohm view yielding deterministic trajectories guided by a pilot wave. In the following note, these approaches are demonstrated as different limits of the same stochastic–variational structure.

# Parisi–Wu

Consider Euclidean quantum mechanics with coordinate \(x(\tau)\) and action
$$
S_E[x] = \int_0^T ds\,
\Big[\tfrac{1}{2}\dot x^2 + V(x)\Big].
$$

Parisi and Wu introduce a fictitious time \(s\) with stochastic partial differential equation
$$
\partial_\tau x(\tau,s)
= -\frac{\delta S_E}{\delta x(\tau,s)} + \eta(\tau,s),
$$
where \(\eta\) is Gaussian white noise with
$$
\langle\eta(\tau,s)\eta(\tau',s')\rangle
  = 2\,\delta(\tau-\tau')\delta(s-s').
$$
The Fokker–Planck equation for the functional probability \(P[x;s]\) is
$$
\partial_s P[x;s]
= \int d\tau\,\frac{\delta}{\delta x(\tau)}
  \left(\frac{\delta}{\delta x(\tau)}+ \frac{\delta S_E}{\delta x(\tau)}\right)P,
$$
with stationary solution \(P_{\mathrm{eq}}[x]\propto e^{-S_E[x]}\).
The \(s\to\infty\) limit reproduces the Euclidean path integral of quantum mechanics.

# Onsager–Machlup / MSRJD

The Parisi and Wu equation is of the form
\(\partial_s x = F[x] + \eta\),
with \(F[x] = \ddot x - V'(x)\).
Let \(\tilde{x}(\tau,s)\) be a response field.
The MSRJD functional integral is
$$
Z = \int \mathcal{D}\!\left[x, \tilde{x}\right] e^{S_{M}[x,\tilde{x}]}
$$
with
$$
S_{M}[x,\tilde{x}]
= \int ds\,d\tau
\left[
  i\tilde x(\partial_s x - \ddot x + V'(x))
  - \tilde x^2
\right].
$$
Integrating over \(\tilde x\) yields the Onsager–Machlup action
$$
S_{O}[x]
= \tfrac{1}{4}\!\int\! ds\,d\tau
  \big(\partial_s x - \ddot x + V'(x)\big)^2
- \tfrac{1}{2}\!\int\! ds\,d\tau\,V''(x).
$$
The most probable path satisfies
\(\partial_s x = \ddot x - V'(x)\),
the deterministic Parisi–Wu relaxation.
As \(s\!\to\!\infty\), the system approaches the equilibrium measure \(e^{-S_E[x]}\).

# Nelson's Stochastic Mechanics

Nelson's stochastic mechanics describes a physical diffusion process in real time \(t\),
$$
dx_t = b_\pm(x_t,t)\,dt + \sqrt{2\nu}\,dW_t^\pm,
\qquad
\nu=\frac{\hbar}{2m},
$$
with forward/backward drifts \(b_\pm = v \pm u\), where
$$
v = \frac{b_+ + b_-}{2} = \frac{1}{m}\nabla S,
\quad
u = \frac{b_+ - b_-}{2} = \nu\nabla\ln\rho.
$$
The symmetric Onsager–Machlup functional for this double diffusion is
$$
S_N[x]
= \frac{1}{4\nu}\int dt\,
  \Big[(\dot x - v)^2 + u^2\Big]
  + \frac{1}{2}\int dt\,\nabla\!\cdot v.
$$
Varying \(S_N\) yields Nelson's stochastic Newton law
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v
   - (u\!\cdot\!\nabla)u
   - \nu\nabla^2 u\big)
= -\nabla V,
$$
which, using \(u=\nu\nabla\ln\rho\), reduces to
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v\big)
= -\nabla(V+Q),
\quad
Q = -\frac{\hbar^2}{2m}\,
    \frac{\nabla^2\sqrt\rho}{\sqrt\rho}.
$$
These results are are equivalent to the Schrödinger equation under
\(\psi=\sqrt\rho\,e^{iS/\hbar}\).

# de Broglie–Bohm

The de Broglie–Bohm (dBB) theory prescribes deterministic trajectories
$$
\dot x = \frac{1}{m} \nabla S,
$$Quantum mechanics admits several representations whose interconnections are often opaque. Parisi–Wu stochastic quantization introduces a computational time evolution toward a Euclidean quantum measure; while Onsager–Machlup (OM) / MSRJD formalisms express stochastic dynamics as path integrals over trajectories. By comparison, Nelson's stochastic mechanics interprets quantum motion as an underlying diffusion in real time; with the de Broglie–Bohm view yielding deterministic trajectories guided by a pilot wave. In the following note, these approaches are demonstrated as different limits of the same stochastic–variational structure.

# Parisi–Wu

Consider Euclidean quantum mechanics with coordinate \(x(\tau)\) and action
$$
S_E[x] = \int_0^T ds\,
\Big[\tfrac{1}{2}\dot x^2 + V(x)\Big].
$$

Parisi and Wu introduce a fictitious time \(s\) with stochastic partial differential equation
$$
\partial_\tau x(\tau,s)
= -\frac{\delta S_E}{\delta x(\tau,s)} + \eta(\tau,s),
$$
where \(\eta\) is Gaussian white noise with
$$
\langle\eta(\tau,s)\eta(\tau',s')\rangle
  = 2\,\delta(\tau-\tau')\delta(s-s').
$$
The Fokker–Planck equation for the functional probability \(P[x;s]\) is
$$
\partial_s P[x;s]
= \int d\tau\,\frac{\delta}{\delta x(\tau)}
  \left(\frac{\delta}{\delta x(\tau)}+ \frac{\delta S_E}{\delta x(\tau)}\right)P,
$$
with stationary solution \(P_{\mathrm{eq}}[x]\propto e^{-S_E[x]}\).
The \(s\to\infty\) limit reproduces the Euclidean path integral of quantum mechanics.

# Onsager–Machlup / MSRJD

The Parisi and Wu equation is of the form
\(\partial_s x = F[x] + \eta\),
with \(F[x] = \ddot x - V'(x)\).
Let \(\tilde{x}(\tau,s)\) be a response field.
The MSRJD functional integral is
$$
Z = \int \mathcal{D}\!\left[x, \tilde{x}\right] e^{S_{M}[x,\tilde{x}]}
$$
with
$$
S_{M}[x,\tilde{x}]
= \int ds\,d\tau
\left[
  i\tilde x(\partial_s x - \ddot x + V'(x))
  - \tilde x^2
\right].
$$
Integrating over \(\tilde x\) yields the Onsager–Machlup action
$$
S_{O}[x]
= \tfrac{1}{4}\!\int\! ds\,d\tau
  \big(\partial_s x - \ddot x + V'(x)\big)^2
- \tfrac{1}{2}\!\int\! ds\,d\tau\,V''(x).
$$
The most probable path satisfies
\(\partial_s x = \ddot x - V'(x)\),
the deterministic Parisi–Wu relaxation.
As \(s\!\to\!\infty\), the system approaches the equilibrium measure \(e^{-S_E[x]}\).

# Nelson's Stochastic Mechanics

Nelson's stochastic mechanics describes a physical diffusion process in real time \(t\),
$$
dx_t = b_\pm(x_t,t)\,dt + \sqrt{2\nu}\,dW_t^\pm,
\qquad
\nu=\frac{\hbar}{2m},
$$
with forward/backward drifts \(b_\pm = v \pm u\), where
$$
v = \frac{b_+ + b_-}{2} = \frac{1}{m}\nabla S,
\quad
u = \frac{b_+ - b_-}{2} = \nu\nabla\ln\rho.
$$
The symmetric Onsager–Machlup functional for this double diffusion is
$$
S_N[x]
= \frac{1}{4\nu}\int dt\,
  \Big[(\dot x - v)^2 + u^2\Big]
  + \frac{1}{2}\int dt\,\nabla\!\cdot v.
$$
Varying \(S_N\) yields Nelson's stochastic Newton law
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v
   - (u\!\cdot\!\nabla)u
   - \nu\nabla^2 u\big)
= -\nabla V,
$$
which, using \(u=\nu\nabla\ln\rho\), reduces to
$$
m\big(\partial_t v + (v\!\cdot\!\nabla)v\big)
= -\nabla(V+Q),
\quad
Q = -\frac{\hbar^2}{2m}\,
    \frac{\nabla^2\sqrt\rho}{\sqrt\rho}.
$$
These results are are equivalent to the Schrödinger equation under
\(\psi=\sqrt\rho\,e^{iS/\hbar}\).

# de Broglie–Bohm

The de Broglie–Bohm (dBB) theory prescribes deterministic trajectories
$$
\dot x = \frac{1}{m} \nabla S,
$$
where \(S\) satisfies the quantum Hamilton–Jacobi equation
$$
\partial_t S + \frac{(\nabla S)^2}{2m} + V + Q = 0.
$$
In the OM/MSRJD representation, the dBB trajectories correspond to extremals of the functional: either the deterministic limit of the Nelson process or the \(s\!\to\!\infty\) stationary flow of the Parisi–Wu process.

# Summary

The Onsager–Machlup / MSRJD formalism provides a single variational language:

1. **Computational time diffusion (Parisi–Wu):** a gradient flow in functional space whose equilibrium measure is \(e^{-S_E}\) with computational diffusion converging to the quantum ensemble,
2. **Real time diffusion (Nelson):** a symmetric stochastic process with equilibrium \(\rho=|\psi|^2\) with real diffusion of stochastic fluctuations around the quantum flow,
3. **Deterministic flow (Bohm):** the extremal trajectories of the same action, obtained when the stochastic term vanishes, yielding deterministic limit mean current lines of the same ensemble.

The quantum potential appears universally as the curvature term generated by the divergence of the drift in the Onsager–Machlup functional.

Applying the Onsager–Machlup / MSRJD method to Parisi–Wu stochastic quantization produces a diffusion in fictitious time \(s\) whose stationary state reproduces quantum mechanics. Applying the same formalism to Nelson's stochastic mechanics yields the physical diffusion equations that reproduce the Schrödinger dynamics. In the deterministic limit, the Onsager–Machlup extremals coincide with de Broglie–Bohm pilot-wave trajectories. In short, stochastic quantization, stochastic mechanics, and the pilot-wave theory are successive reductions of a single stochastic–variational framework defined by the Onsager–Machlup action.
where \(S\) satisfies the quantum Hamilton–Jacobi equation
$$
\partial_t S + \frac{(\nabla S)^2}{2m} + V + Q = 0.
$$
In the OM/MSRJD representation, the dBB trajectories correspond to extremals of the functional: either the deterministic limit of the Nelson process or the \(s\!\to\!\infty\) stationary flow of the Parisi–Wu process.

