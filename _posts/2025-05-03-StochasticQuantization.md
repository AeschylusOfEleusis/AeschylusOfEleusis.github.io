---
layout:   post
title: "Stochastic Quantization"
date: 2025-05-03 10:00:00 +0800
categories: [Quantum Field Theory]
tags: [Stochastic Quantization, Numerical Relativity,Quantum Field Theory, Stochastic Calculus, Triviality, Blackholes, NonequilibriumQFT, PathIntegrals, Foundations QM]
math:       true        # enable KaTeX
---
# Notes on Stochastic Quantization (Draft)

## Abstract

A view of stochastic quantization is sketched here; written from the perspective of numerical relativity. Examples from mathematical physics are considered as illustration.

Let the field $\Phi^{\mathfrak{k}}\bigl(s, x^{a}\bigr)$ satisfy a principle of stationary action with classical equations of motion

$$
\frac{\delta }{\delta \Phi^{\mathfrak{k}}} S\left[\Phi^{\mathfrak{m}}\left(s,x^{a}\right)\right] = 0.
$$


In this notation, the background spacetime is $x^{a} = (t,x^{i})$ with $n-1$ spatial dimensions,  and the index $\mathfrak{k}$ indicates internal symmetries.  Let $s$ be time of stochastic evolution and let $\xi^{\mathfrak{k}}(s,x^{d})$ be a vector of general noise indexed over the internal symmetry.  The stochastic partial differential equation of stochastic quantization is

$$
\frac{\partial}{\partial s} \Phi^{\mathfrak{k}}\bigl(s, x^{a}\bigr) = \frac{\delta }{\delta \Phi^{\mathfrak{k}}} S\left[\Phi^{\mathfrak{m}}\bigl(s, x^{a}\bigr)\right] + \xi^{\mathfrak{k}}\bigl(s,x^{a}\bigr).
$$

Most commonly, gaussian noise $\xi^{\mathfrak{k}}\bigl(s,x^{a}\bigr)$ is considered  in study of stochastic partial differential equations; although  non-gaussian and L\'evy type noise are handled analogously.


Consider the following action for a spacetime scalar field (indexed by $\mathfrak{k}$ over the internal symmetry) 

$$
S\bigl[\Phi^{\mathfrak{i}}\bigr] = \int d^{n}x\bigl\{ \mathfrak{g}_{\mathfrak{j} \mathfrak{k}}\nabla_{a} \Phi^{\mathfrak{j}} g^{ab}  \nabla_{b}  \Phi^{\mathfrak{k}} - U\bigl(\Phi^{\mathfrak{i}}\bigr)\bigr\}
$$

where

- $g^{ab}(x^{c})$ is a metric of the background spacetime manifold $\mathcal{M}$,
- $\mathcal{A}_{b}$ is a connection field of a gauge-symmetry fibre bundle $\mathcal{E}$ over $\mathcal{M}$,
- $\nabla_{a} \equiv \partial_{a} - \mathcal{A}_{a}$ is the covariant derivative of the connection,
- $\mathfrak{g}_{\mathfrak{j}\mathfrak{k}}$ governs the trace over the internal symmetry, and
- $U(\Phi^{\mathfrak{j}})$ is a generalized potential governing dynamics and self-interactions.

This example is sufficient to study effects of:

1. The background spacetime geometry (base manifold dimension, topology, curvature, etc),
2. The gauged internal symmetry,
3. The parameter-space survey of the dynamical system (stationary states, instabilities, symmetry breaking, etc).



For example, in the limit of zero spatial dimensions ($n=1$), quantum mechanics is formulated as the following stochastic PDE:

$$
\frac{\partial}{\partial s}\,x^{\mathfrak{i}}(s,\tau) = -\,\frac{\delta}{\delta x^{\mathfrak{i}}}\,S\bigl[x^{\mathfrak{j}}(s,\tau)\bigr] + \xi^{\mathfrak{i}}(s,\tau),
$$

where 

$$
S[x^{\mathfrak{l}}] = \int dt'\;\bigl\{\mathfrak{g}_{\mathfrak{i}\mathfrak{j}} \dot{x}^{\mathfrak{i}}\dot{x}^{\mathfrak{j}} + A_{\mathfrak{k}}\,\dot{x}^{\mathfrak{k}} - U(x^{\mathfrak{l}})\bigr\}.
$$

[Here $\dot{x}^{\mathfrak{i}} \equiv \frac{d }{d\tau} x^{\mathfrak{i}}(\tau)$ with $\tau$ either denoting 'clock on the wall' Newtonian time in the non relativistic limit or 'proper time' in the relativistic limit.]

This generic formalism applies to study of:

- Foundations of quantum mechanics,
- Path integration,
- Non-equilibrium statistical mechanics.

More specifically, this approach permits numerical analysis of:

- The effective action functional and functional renormalization group,
- The path integral of the non-relativistic particle on a curved base manifold,
- The path integral of the relativistic particle in a curved (pseudo-Riemannian) or flat (Minkowski) spacetime,
- Quantum chaos.

---

For base manifolds with dimension $n \ge 2$, stochastic quantization enables study of general problems in quantum field theory.  For example, on a flat Minkowski background the following problems are of immediate interest:

- Conformal field theories in $1+1$ dimensions,
- Fractional quantum Hall effect and Chern–Simons theory in $2+1$ dimensions,
- “Triviality” of the self-interaction $U(\Phi)=\lambda\left[\Phi^{2}\right]^{2}_{4}$ in $3+1$ dimensions.

Fractional noise effects in quantum field theories is an additional direction, introducing fractional noise in the context of the functional integral.

---

From numerical relativity, the equations of motion of a free scalar field on a spherically symmetric spacetime background are

$$
\frac{\partial \Phi}{\partial t} = \frac{\partial}{\partial r}\bigl(\tfrac{\alpha}{a}\,\Pi\bigr),
$$

$$
\frac{\partial \Pi}{\partial t} = 3\,\frac{\partial}{\partial r^{3}}\Bigl(r^{2}\,\tfrac{\alpha}{a}\,\Phi\Bigr),
$$

$$
\Phi(r,t) \equiv \frac{\partial \Phi}{\partial r},
$$

$$
\Pi(r,t) \equiv \frac{a}{\alpha}\,\frac{\partial \Phi}{\partial t},
$$

where the Einstein equations reduce to the constraints

$$
\frac{a'}{a} + \frac{a^{2}-1}{2r} - 2\pi r\bigl(\Phi^{2} + \Pi^{2}\bigr) = 0,
$$

$$
\frac{\alpha'}{\alpha} - \frac{a^{2}-1}{2r} - 2\pi r\bigl(\Phi^{2} + \Pi^{2}\bigr) = 0.
$$

Example problems to consider here include $a$ and $\alpha$ fixed as the Schwarzschild solution (black hole physics) or deSitter
space (cosmology of the early universe). Then, the dynamics of the associated stochastic partial differential equations correspond
to quantum field theory on a curved spacetime. However, when the dynamics of the back reaction of the gravitational field are
included  (by simultaneous solution of Einstein's equations) the result is a quantum theory of gravity; approached in the context
of numerical relativity and stochastic quantization. As an intermediate step, scalar fields and the associated BTZ black holes in
lower dimensional 2+1 gravity are natural to consider in this numerical approach. 

**To be continued ...**
## References

| ID  | Link                                                                                                                                                                                                                                                                              | Notes                                                                                                                            |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| S1  | [Martin et al “Statistical Dynamics of Classical Systems” 1973](https://journals.aps.org/pra/abstract/10.1103/PhysRevA.8.423)                                                                                                                                                        | Develops a formalism for the statistical treatment of classical many-body systems, including fluctuating forces and dissipation. |
| S2  | [Hohenberg and Halperin “Theory of Dynamic Critical Phenomena” 1977](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.49.435)                                                                                                                                             | Reviews the classification and scaling behavior of dynamic critical processes near second-order phase transitions.               |
| S3  | [Fox “Gaussian stochastic processes in physics” 1978](https://www.sciencedirect.com/science/article/abs/pii/037015737890145X)                                                                                                                                                      | Explores the mathematical properties and physical applications of Gaussian stochastic processes in diverse physical systems.     |
| S4  | [Zhou et al “Closed time path Green’s functions and critical dynamics” 1980](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.22.3385)                                                                                                                                       | Introduces the closed time path (CTP) Green’s function formalism to study nonequilibrium critical dynamics.                       |
| S5  | [Parisi Wu “Perturbation Theory Without Gauge Fixing” 1980](https://inspirehep.net/literature/9589)                                                                                                                                                                               | Proposes a stochastic quantization approach that avoids explicit gauge fixing by introducing auxiliary time variables.            |
| S6  | [Seiler “Stochastic Quantization and Gauge Fixing” 1984](https://link.springer.com/chapter/10.1007/978-3-7091-8780-7_11)                                                                                                                                                            | Analyzes the relationship between stochastic quantization techniques and conventional gauge-fixing procedures.                     |
| S7  | [J. Zinn-Justin “Renormalization and stochastic quantization” 1986](https://www.sciencedirect.com/science/article/abs/pii/0550321386905924)                                                                                                                                         | Investigates the renormalization of quantum field theories within the stochastic quantization framework.                            |
| S8  | [Rumpf “Stochastic Quantization of Einstein Gravity” 1986](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.33.942)                                                                                                                                                         | Applies stochastic quantization to the gravitational field, exploring potential routes to quantize Einstein’s theory.             |
| S9  | [Goldschmidt “Decay of Magnetization” 1987](https://www.sciencedirect.com/science/article/abs/pii/055032138790352X)                                                                                                                                                                 | Studies the time-dependent decay of magnetization near critical points using stochastic and renormalization methods.               |
| S10 | [Damgaard and Huffel “Stochastic Quantization”](https://homepage.univie.ac.at/helmuth.hueffel/PhysRep.pdf)                                                                                                                                                                        | Provides a comprehensive review of stochastic quantization techniques and their applications in field theory.                      |
| S11 | [Hu et al “Quantum Brownian Motion I” 1992](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.45.2843)                                                                                                                                                                        | Develops an influence functional approach for analyzing quantum Brownian motion of a system coupled to a thermal bath.            |
| S12 | [Namiki “Stochastic Quantization” 1992](https://link.springer.com/book/10.1007/978-3-540-47217-9)                                                                                                                                                                                  | Monograph detailing the foundations and various applications of stochastic quantization in quantum field theory.                   |
| S13 | [Hu et al “Quantum Brownian Motion II” 1993](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.47.1576)                                                                                                                                                                       | Extends the quantum Brownian motion framework to relativistic fields and investigates decoherence processes.                        |
| S14 | [Namiki “Basic Ideas” 1993](https://academic.oup.com/ptps/article/doi/10.1143/PTPS.111.1/1889428)                                                                                                                                                                                   | Outlines the fundamental concepts underlying stochastic quantization, with emphasis on gauge theories.                            |
| S15 | [Berges “Noneqilbrium QFT” 2005](https://arxiv.org/abs/hep-lat/0508030)                                                                                                                                                                                                              | Reviews theoretical techniques for studying nonequilibrium quantum field dynamics using functional methods.                        |
| S16 | [Hirayama “Classical Simulation of QFT I” 2005](https://arxiv.org/abs/hep-th/0507126)                                                                                                                                                                                               | Proposes a classical lattice simulation scheme for out-of-equilibrium quantum fields based on classical statistical analogies.    |
| S17 | [Hirayama et al “Classical Simulation of QFT II” 2005](https://arxiv.org/abs/hep-lat/0507014)                                                                                                                                                                                      | Extends classical simulation methods to non-Abelian gauge theories, demonstrating feasibility in lattice frameworks.                |
| S18 | [Berges and Sexty “Gauge theory simulations” 2007](https://arxiv.org/abs/0708.0779)                                                                                                                                                                                                 | Presents real-time lattice simulations of gauge theories using classical-statistical approximations to explore thermalization.    |
| S19 | [de Aguiar et al “Scalar fields in de Sitter” 2008](https://arxiv.org/abs/0809.2273)                                                                                                                                                                                                  | Examines stochastic dynamics and correlation functions of scalar fields propagating in de Sitter spacetime.                        |
| S20 | [Hu and Verdaguer “Stochastic Gravity” 2008](https://arxiv.org/abs/0802.0658)                                                                                                                                                                                                        | Provides a comprehensive review of stochastic gravity, where metric fluctuations are driven by quantum stress-energy noise.         |
| S21 | [Guralnik and Pehlevan “Complex Langevin and Shwinger Dyson” 2007](https://arxiv.org/abs/0710.3756)                                                                                                                                                                                 | Investigates complex Langevin methods as a means to solve nonperturbative Schwinger-Dyson equations in quantum field theory.        |
| S22 | [Kamenev and Levchenko “Keldysh and sigma models” 2009](https://arxiv.org/abs/0901.3586)                                                                                                                                                                                            | Reviews the Keldysh nonequilibrium formalism and its connection to nonlinear sigma models in condensed matter and field theory.    |
| S23 | [De Dominicis and Giardina “Random Fields and Spin Glasses” 2009](https://www.cambridge.org/core/books/random-fields-and-spin-glasses/06E0CACD41F11FC90716329F5016B0E1)                                                                                                               | Textbook covering theoretical methods—such as replica and functional approaches—for random fields and spin glass phenomena.         |
| S24 | [Aarts et al “Instabilities in complex Langecin” 2009](https://arxiv.org/abs/0912.0617)                                                                                                                                                                                             | Studies numerical instabilities arising in complex Langevin simulations of quantum field theories with severe sign problems.       |
| S25 | [Iso and Okazawa “Stochastic equations on blackhole backgrounds” 2011](https://arxiv.org/abs/1104.2461)                                                                                                                                                                            | Formulates stochastic differential equations for quantum fields in black hole spacetimes to explore horizon fluctuations.          |
| S26 | [Cassol-Seewald et al “Landau Ginzburg” 2012](https://www.worldscientific.com/doi/abs/10.1142/S0129183112400165?srsltid=AfmBOopK9a_cFzkM1umzysl2uAi-IFnMiyzqg1c7lQJx_UoJh5rOGbs9)                                                                           | Applies stochastic quantization techniques to the Landau–Ginzburg model and analyzes critical scaling behavior.                    |
| S27 | [Seiler “Complex Langevin” 2017](https://arxiv.org/abs/1708.08254)                                                                                                                                                                                                                   | Reviews advances and challenges in complex Langevin methods for tackling complex action problems in lattice field theories.        |
| S28 | [Berger et al “Sign problem” 2019](https://arxiv.org/abs/1907.10183)                                                                                                                                                                                                                 | Surveys state-of-the-art approaches—such as Lefschetz thimbles and complex Langevin—to mitigate the sign problem in lattice QCD.  |
| S29 | [Antonio dos Reis et al “Semiclassical Gravity” 2018](https://arxiv.org/abs/1804.04569)                                                                                                                                                                                              | Develops semiclassical approximation schemes for gravity coupled to quantum fields, focusing on backreaction effects.             |
| S30 | [Hu and Verdaguer “Semiclassical and Stochastic Gravity” 2020](https://www.cambridge.org/core/books/semiclassical-and-stochastic-gravity/E3F88C9655023210C93ECCEE8ADEC199#)                                                                         | Updates the theoretical framework blending semiclassical gravity with stochastic metric fluctuations for early-universe studies.    |
| S31 | [Cai et al “Regulariztion of Complex Langevin” 2021](https://arxiv.org/abs/2109.12762)                                                                                                                                                                                               | Proposes novel regularization techniques to improve convergence and reliability of complex Langevin simulations in field theories. |
| S32 | [Hiryama “Classical simulation of QFT” 2024](https://arxiv.org/abs/1912.01648)                                                                                                                                                                                                      | Reviews classical-statistical lattice methods for simulating real-time quantum field dynamics in various contexts.                 |