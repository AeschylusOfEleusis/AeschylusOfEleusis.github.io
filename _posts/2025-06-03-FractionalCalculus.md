---
layout:   post
title: "Fractional Calculus"
date: 2025-06-03 10:00:00 +0800
categories: [Computational Finance]
tags: [Probability Information Risk, Quantum Field Theory, Black holes, Path Integrals, Stochastic Calculus, Computational Finance, Scientific Computing]
math:       true        # enable KaTeX
---

# Notes on Fractional Calculus (Draft)

## Abstract

Resources concerning alpha-stable Lévy distributions are provided with consideration of associated fractional operators and their calculus. Several domains of classical and quantum physics are then considered from a fractional perspective. The notes that follow trace a conceptual pipeline: heavy-tailed stochastic processes motivate non-local operators, which in turn generalize the calculus of variations, spacetime geometry, and quantum theory. Twenty-seven references, spanning from foundational mathematics through speculative theoretical physics, are surveyed and situated within this pipeline. Emphasis is placed on operator definitions, their interrelations, and the physical content of fractional generalizations.

---

## 1. Introduction

The extension of the derivative $D^n$ from integer order $n$ to arbitrary order $\alpha$ is not a recent idea. Leibniz himself, in a 1695 letter to l'Hôpital, speculated about the meaning of $d^{1/2}y/dx^{1/2}$, remarking that it "will lead to a paradox, from which one day useful consequences will be drawn." The paradox has since resolved into a coherent—if still expanding—mathematical theory, and the useful consequences now reach from viscoelastic materials science through mathematical finance to quantum gravity.

These notes survey the literature assembled on the project page for fractional calculus, organized as a guided reading path through twenty-seven sources. The structure follows the logic of the subject itself: one begins with the stochastic processes (Lévy flights) whose generators are fractional operators, proceeds to the mathematical apparatus of those operators, and then follows the operators into classical mechanics, gravity, and quantum theory. The intent is not to teach fractional calculus from first principles—several of the references surveyed here do that with more authority—but to provide an idiosyncratic map of the territory, noting where the major results live, how the different formalisms relate, and where the ground shifts from established mathematics to speculative physics.

A word on scope. The sources collected here are weighted toward the physics side: stochastic processes, path integrals, and field theory. The engineering applications of fractional calculus—control theory, signal processing, biomedical modeling—are represented only through the textbook references in Section 3. Readers whose interests lie in those directions will find the textbooks (particularly Kilbas et al. and Sabatier et al.) adequate starting points, but should expect to supplement the bibliography with domain-specific literature.

The notes are organized as follows. Section 2 treats Lévy flights and their financial applications. Section 3 covers the mathematical foundations of fractional operators. Section 4 addresses classical physics applications, including fractional mechanics and gravity. Section 5 develops the quantum applications: fractional Schrödinger equations, Lévy path integrals, and fractional quantum field theory. Section 6 extracts the core mathematical framework that runs through all four application domains. Section 7 identifies the cross-cutting themes—non-locality, anomalous scaling, and dimensional flow—that unify the literature. Section 8 provides a critical assessment, including the status of various conjectures and recommendations for further reading.

---

## 2. Lévy Flights and Financial Applications

### 2.1 Motivation: Beyond Brownian Motion

The classical random walk, in its continuum limit, produces Brownian motion: Gaussian increments, finite variance, and mean-squared displacement growing linearly with time. Many physical and financial systems do not behave this way. Asset returns exhibit heavy tails and occasional extreme moves. Particles in disordered media sometimes undergo anomalous diffusion, with mean-squared displacement scaling as $\langle x^2 \rangle \sim t^{2/\alpha}$ for some $\alpha \neq 2$. Lévy flights—random walks whose step lengths are drawn from heavy-tailed, alpha-stable distributions—provide the natural mathematical framework for these phenomena.

The connection to fractional calculus is direct: the infinitesimal generator of a symmetric $\alpha$-stable Lévy process is the fractional Laplacian $(-\Delta)^{\alpha/2}$. This operator, defined precisely in Section 6, is the bridge between the stochastic processes of this section and the differential equations of Sections 3 through 5. The reader who wishes to understand why fractional operators appear throughout physics and finance should begin here.

### 2.2 The Physics of Anomalous Diffusion

**S1: Bouchaud & Georges (1990).** "Anomalous Diffusion in Disordered Media," *Physics Reports* 195, 127–293.

This comprehensive review established the theoretical framework for understanding transport in disordered systems and remains the anchor reference for the physics side of anomalous diffusion. Bouchaud and Georges classify diffusion regimes according to how the mean-squared displacement $\langle x^2(t) \rangle$ scales with time: subdiffusion ($\langle x^2 \rangle \sim t^\beta$ with $\beta < 1$), normal diffusion ($\beta = 1$), and superdiffusion ($\beta > 1$, including ballistic transport). Lévy flights correspond to the superdiffusive case, where the divergence of the step-length variance produces anomalous scaling.

The paper's lasting contribution is the connection between microscopic disorder—random trapping times, quenched random potentials, percolation clusters—and the macroscopic transport laws that emerge. For present purposes, the key result is that certain disorder distributions produce Lévy flight processes as their continuum limits, with the disorder controlling the stability index $\alpha$. This provides the physical motivation for the mathematical apparatus that follows.

**S5: Chechkin, Metzler, Klafter & Gonchar (2008).** "Introduction to the Theory of Lévy Flights," Wiley chapter.

Where Bouchaud and Georges write for the research physicist, Chechkin et al. provide a more accessible pedagogical introduction. The chapter systematically develops Lévy stable distributions, discusses their defining properties (self-similarity, infinite divisibility, generalized central limit theorems), and surveys applications across physics and complex systems. Topics include turbulence, anomalous diffusion in plasmas, and search strategies in foraging animals.

This is a reasonable starting point for a reader who wants the essential definitions and properties of alpha-stable distributions before encountering them in the financial or physical literature. The treatment is not as deep as Bouchaud and Georges, but it covers the ground more efficiently.

### 2.3 Financial Applications: Jump-Diffusion and Lévy Models

The application of Lévy processes to finance reflects the empirical observation that asset returns are not Gaussian: they exhibit heavy tails, skewness, and occasional large discontinuous moves ("jumps") that Brownian motion cannot accommodate. The references in this section develop progressively more sophisticated models that incorporate these features.

**S2: Duffie, Pan & Singleton (2000).** "Transform Analysis and Asset Pricing for Affine Jump-Diffusions," SSRN.

A note on labeling: the project page identifies this reference as "SVJJ" (Stochastic Volatility with Joint Jumps), which is informal shorthand. The linked SSRN paper is titled "Transform Analysis and Asset Pricing for Affine Jump-Diffusions" and treats a broader class of models. The SVJJ model is a specific instance within the affine jump-diffusion framework that Duffie, Pan, and Singleton develop.

The paper's contribution is methodological: it provides a unified transform-based approach to pricing derivatives in models where the state vector follows an affine jump-diffusion process. The key technical result is that the characteristic function of affine processes satisfies a system of generalized Riccati ODEs, which can be solved (often in closed form) to yield option prices via Fourier inversion. This framework subsumes Black-Scholes, Heston, and various jump-diffusion models as special cases.

For the present notes, the paper matters because it sits at the interface between Lévy-type jump processes and practical derivative pricing—the same interface that Carr et al. develop from a different angle.

**S3: Carr, Geman, Madan & Yor (2003).** "Stochastic Volatility for Lévy Processes," *Mathematical Finance*.

**S4: Carr & Wu (2005).** "Time-Changed Lévy Processes and Option Pricing," NYU working paper.

These two papers from the NYU group develop stochastic volatility frameworks driven by pure-jump Lévy processes. The 2003 paper formulates three specific Lévy processes—Normal Inverse Gaussian (NIG), Variance Gamma (VG), and CGMY—with stochastic volatility induced by CIR (Cox-Ingersoll-Ross) time changes. The mathematical centerpiece is the derivation of explicit characteristic functions for the time-changed processes, which enables efficient Fourier-based option pricing.

A point of mathematical substance in the 2003 paper deserves emphasis: the distinction between martingale marginals and martingale measures. A process whose marginal distributions are consistent with a martingale is not necessarily a martingale, because the joint distribution matters. This subtlety is easy to overlook but has consequences for arbitrage-free pricing.

The 2005 paper extends the framework through general time-changed Lévy processes, providing more flexible models that can separately capture stochastic volatility and jump dynamics. Together, these papers represent the state of the art in Lévy-based option pricing as of the mid-2000s.

**S6: Platen & Bruti-Liberati (2010).** *Numerical Solution of Stochastic Differential Equations with Jumps in Finance*, Springer.

A note on dating: the project page lists this as 2017, but the Springer copyright page indicates 2010.

This monograph provides comprehensive numerical methods for jump-diffusion SDEs, covering strong and weak approximation schemes, Monte Carlo simulation techniques, and multi-level methods. It is the implementation companion to the theoretical work of S2–S4: once one has a Lévy-based model, one needs to simulate it, and this book tells you how. Topics include Euler and Milstein schemes for jump-diffusions, variance reduction, and the treatment of infinite-activity Lévy processes (where jumps arrive at an infinite rate but remain summable).

### 2.4 Reading Path for This Section

A reader approaching Lévy processes for the first time should begin with Chechkin et al. (S5) for definitions and intuition, then Bouchaud and Georges (S1) for physical depth. The financial applications are best approached through Carr et al. (S3) before Duffie et al. (S2), since the Lévy-process framework in S3 makes the affine structure of S2 more transparent. Platen and Bruti-Liberati (S6) is consulted as needed for numerical implementation.

---

## 3. Fractional Calculus: Mathematical Foundations

### 3.1 The Central Question

The extension $D^n \to D^\alpha$ for $\alpha \in \mathbb{R}$ (or $\mathbb{C}$) is not unique. Multiple definitions of fractional differentiation exist, each with different domains of applicability, different treatment of boundary conditions, and different physical interpretations. The references in this section develop the major constructions—Riemann-Liouville, Caputo, Grünwald-Letnikov, and spectral (Fourier)—and the special functions that arise as solutions to fractional differential equations.

The multiplicity of definitions is not a defect but a feature: different physical situations call for different formulations. The Riemann-Liouville derivative is the natural generalization from integral transforms; the Caputo derivative handles initial conditions in the manner familiar from integer-order ODEs; the spectral definition via Fourier transform connects most directly to Lévy processes and the fractional Laplacian.

### 3.2 Wheeler's Lecture Notes (S7–S10)

Nicholas Wheeler (Reed College) produced four detailed lecture notes between 1997 and 2005 that provide exceptional pedagogical clarity and are freely accessible as PDFs from the Reed College website. These notes are among the most valuable resources in the entire bibliography, precisely because they are written by a physicist for physicists, with careful attention to both mathematical rigor and physical motivation.

**S7: "Construction and Physical Application of the Fractional Calculus" (1997).**

The first installment develops foundational constructions through multiple approaches. Wheeler begins with Lacroix's observation (1819) that the formula $D^m x^p = \frac{\Gamma(p+1)}{\Gamma(p-m+1)} x^{p-m}$, valid for integer $m$, extends naturally to non-integer $m$ via the Gamma function. He then develops Grünwald's construction (1867), which starts from the difference quotient definition of the derivative and replaces the binomial coefficients with their Gamma-function generalizations:

$$D^\alpha f(x) = \lim_{h \to 0} \frac{1}{h^\alpha} \sum_{k=0}^{\infty} (-1)^k \binom{\alpha}{k} f(x - kh)$$

The central achievement is the Riemann-Liouville integral of order $\nu > 0$:

$${}_a D^{-\nu}_x f(x) = \frac{1}{\Gamma(\nu)} \int_a^x (x-y)^{\nu-1} f(y) \, dy$$

This formula reduces iterated integration (integrating $f$ a total of $n$ times) to a single integral transform, and it does so for arbitrary real order $\nu$. The proof that it reproduces $n$-fold integration when $\nu = n$ is a pleasant exercise in properties of the Beta function.

Wheeler then discusses two historically significant applications that illustrate the power and naturalness of fractional methods.

*Abel's tautochrone problem (1823).* The problem asks: for what curve is the time of frictionless descent under gravity independent of the starting height? Abel recognized that the constraint equation takes the form of a fractional integral equation and solved it via semi-differentiation (application of $D^{1/2}$), obtaining the cycloid. This was, historically, the first application of fractional calculus to a physical problem.

*Heaviside's telegraph equation (1893).* Heaviside used operational calculus involving $D^{1/2}$ to analyze the diffusion equation governing signal propagation in telegraph cables. His methods, controversial at the time, anticipated modern fractional techniques and yield correct results for the heat kernel.

Wheeler also develops the application to Klein-Gordon Green's functions, demonstrating Riesz's "method of dimensional ascent": the Green's function for the wave equation in $n+1$ dimensions can be obtained from the Green's function in lower dimensions by application of a fractional integral operator. This is a striking example of how fractional operators connect solutions across dimensions.

**S8: "Fractional Leibniz" (1997).**

The second installment addresses the product rule for fractional derivatives. In integer-order calculus, Leibniz's rule gives $D^n(fg) = \sum_{k=0}^{n} \binom{n}{k} D^k f \cdot D^{n-k} g$. The fractional generalization replaces the finite sum with an infinite series:

$$D^\alpha(fg) = \sum_{k=0}^{\infty} \binom{\alpha}{k} D^k f \cdot D^{\alpha - k} g$$

where the binomial coefficient $\binom{\alpha}{k} = \frac{\Gamma(\alpha+1)}{\Gamma(k+1)\Gamma(\alpha-k+1)}$ is now defined via the Gamma function for non-integer $\alpha$. The convergence conditions for this series, the circumstances under which it truncates, and the interplay between left-sided and right-sided fractional derivatives are all treated with care.

**S9: "Fractional Laplacian" (1998).**

The third installment develops the fractional Laplacian $(-\Delta)^{\alpha/2}$, which is the central operator connecting the stochastic processes of Section 2 with the quantum mechanics of Section 5. Wheeler approaches the fractional Laplacian through its spectral (Fourier) definition and connects it to the Riesz potential. The relationship between the fractional Laplacian, the Riesz derivative, and the generators of stable Lévy processes is made explicit—this is the mathematical link that the entire bibliography depends on.

**S10: "Alternative Approach" (2005).**

The fourth installment, written eight years after the first three, proposes alternative constructions and interpretations of fractional differentiation and integration. This note is more exploratory in character and reflects the continued evolution of Wheeler's thinking about the subject.

### 3.3 Comprehensive Textbooks and Monographs (S11–S14)

**S11: Kilbas, Srivastava & Trujillo (2006).** *Theory and Applications of Fractional Differential Equations*, Elsevier.

This is the standard reference work in the field—the book one cites when establishing that a result is "well known" in fractional calculus. Coverage includes:

- Riemann-Liouville, Caputo, and Hadamard derivatives, with their domains, interrelations, and composition rules.
- Mittag-Leffler and Wright functions, which play the role in fractional calculus that the exponential function plays in integer-order calculus.
- Existence and uniqueness theory for linear and nonlinear fractional differential equations.
- Laplace and Fourier transform methods for fractional equations.
- Applications to viscoelasticity, control theory, and anomalous diffusion.

A reader working through any of the physics applications in Sections 4 and 5 will eventually need to consult Kilbas for precise statements of operator identities and composition rules.

**S12: Sabatier, Agrawal & Machado, eds. (2007).** *Advances in Fractional Calculus*, Springer.

This edited volume compiles research developments across multiple disciplines. The table of contents indicates coverage of Caputo derivative initialization (a subtle point: what initial conditions should one impose for a Caputo fractional ODE?), numerical discretization schemes, and applications across mechanics, diffusion, and signal processing. Edited volumes are necessarily uneven, but this one serves as a useful map of the field's breadth as of the mid-2000s.

**S13: Zhou, Wang & Peng (2016).** *Basic Theory of Fractional Differential Equations*, 2nd ed., World Scientific.

**S14: Baleanu, Diethelm, Scalas & Trujillo (2017).** *Fractional Calculus: Models and Numerical Methods*, 2nd ed., World Scientific.

These two World Scientific volumes emphasize, respectively, qualitative theory (existence, uniqueness, stability) and numerical methods (discretization schemes, spectral methods, finite element approaches for fractional PDEs). Zhou's text includes variational iteration, homotopy perturbation, and Adomian decomposition methods—analytical approximation techniques that are particularly useful when exact solutions are unavailable. Baleanu et al. provide the numerical complement, covering finite-difference discretizations of fractional derivatives, spectral collocation methods, and error analysis.

A note on dating: the project page lists S14 as 2017, which may refer to a reprint or second edition; the original edition appeared in 2012.

### 3.4 What Is Not Covered

The bibliography's treatment of fractional calculus foundations is weighted toward Riemann-Liouville constructions (via Wheeler) and comprehensive textbook references. Several topics that a systematic treatment would include are absent or underrepresented:

- The **Caputo derivative** receives dedicated coverage in the textbooks (particularly Kilbas) but not in the standalone references. For initial-value problems, the Caputo formulation is often preferred because it permits conventional (integer-order) initial conditions.
- **Fractional Brownian motion**, a Gaussian process with long-range dependence, is related to but distinct from the Lévy processes of Section 2. It does not appear in the bibliography.
- **Mittag-Leffler functions** are discussed in the textbooks but not given a dedicated reference. For a reader encountering $E_\alpha(z)$ for the first time, Gorenflo, Kilbas, Mainardi, and Rogosin's *Mittag-Leffler Functions, Related Topics and Applications* (Springer, 2014) would be a useful supplement.
- The **Grünwald-Letnikov** definition, while developed in Wheeler's S7, is not represented in the more recent textbook literature surveyed here.

### 3.5 Reading Path for This Section

Begin with Wheeler's S7 for historical motivation and the Riemann-Liouville construction, then S9 for the fractional Laplacian. Consult Kilbas (S11) as needed for precise operator identities. The numerical methods in Baleanu (S14) become relevant when one begins implementing fractional models computationally.

---

## 4. Applications in Classical Physics

### 4.1 Overview

The references in this section apply fractional calculus to two distinct areas: classical mechanics (Lagrangian and Hamiltonian formulations with fractional derivatives) and gravitational theory (fractional modifications of spacetime geometry). The conceptual transition from Section 3 is significant: we move from "fractional operators as tools for solving equations" to "fractional operators as part of the physics itself"—either as descriptions of non-conservative or memory-dependent dynamics, or as features of the spacetime geometry.

### 4.2 Fractional Mechanics (S15–S16)

**S15: Cresson (2006).** "Fractional embedding of differential operators and Lagrangian systems," arXiv:math/0605752.

A clarification on the project page's label: the page calls this "Fractional Lagrangian Mechanics," but the linked paper's actual title and content concern "fractional embedding." The distinction matters. Cresson's contribution is an embedding-theory approach: he defines a "fractional embedding" that maps ordinary differential operators into fractional ones, constructs a symmetric operator from left and right Riemann-Liouville derivatives, and derives fractional versions of the Euler-Lagrange equations, Noether's theorem, and the Hamiltonian formalism.

The physical motivation is that classical mechanics assumes differentiable trajectories, but physical systems may follow non-differentiable paths (as in Brownian motion or, more speculatively, at quantum scales). Cresson's embedding provides a principled way to extend variational mechanics to this setting, connecting to earlier work by Riewe on non-conservative Lagrangian systems.

The paper also raises a mathematical subtlety that recurs throughout fractional mechanics: the interplay between left-sided and right-sided fractional derivatives. In integer-order calculus, there is no distinction (modulo a sign), but in fractional calculus, the left Riemann-Liouville derivative ${}_a D^\alpha_t$ and the right derivative ${}_t D^\alpha_b$ are genuinely different operators. Cresson's symmetrized combination is one approach to resolving this asymmetry; other approaches exist and lead to different physics.

**S16: Atanacković, Pilipović, Stanković & Zorica (2014).** *Fractional Calculus with Applications in Mechanics*, Wiley.

A note on dating: the project page lists this as 2004, but the Wiley catalog indicates a 2014 publication date.

This comprehensive treatise develops fractional viscoelasticity, wave propagation in fractional media, and fractional oscillators. The central physical idea is that many real materials exhibit memory effects: the stress at the present time depends not only on the current strain but on the entire strain history, weighted by a power-law kernel. Fractional constitutive relations—relating stress to fractional derivatives of strain—capture this behavior naturally.

The power-law relaxation function $G(t) \sim t^{-\alpha}$ is the signature of fractional viscoelasticity. Integer-order models (springs and dashpots, i.e., Maxwell and Voigt models) produce exponential relaxation, which decays too rapidly to match experimental data for polymers, biological tissues, and geological materials. Fractional models interpolate between elastic ($\alpha = 0$) and viscous ($\alpha = 1$) behavior with a single parameter.

### 4.3 Fractional Gravity and Multifractional Spacetime (S17–S20)

This group of references represents a significant escalation in speculative content. While fractional mechanics (S15–S16) applies established mathematical tools to experimentally accessible systems, fractional gravity applies them to spacetime itself—a domain where direct experimental tests are, at present, extremely limited.

**S17: Vacaru (2010).** "Fractional Dynamics from Einstein Gravity, General Solutions, and Black Holes," arXiv:1004.0628.

The project page labels this "Fractional Blackholes," which is informal but captures the content. Vacaru investigates how fractional calculus can be integrated into the geometry of spacetime, using the Caputo derivative on nonholonomic manifolds. The paper constructs fractional deformations of Schwarzschild and Kerr black hole solutions.

A clarification: the first document in the source material (the "Analysis" document) identified this paper as "Fractional Nonholonomic Ricci Flows." That is a different Vacaru paper (arXiv:1004.0625). The paper actually linked on the project page is 1004.0628, which concerns fractional dynamics and black holes. The two papers are related—both deal with fractional geometry on nonholonomic manifolds—but they are distinct.

**S18–S20: Calcagni's Multifractional Spacetime Program (2010–2013).**

Gianluca Calcagni has developed a systematic program exploring what happens when the dimensionality of spacetime is not fixed but scale-dependent—a scenario motivated by several approaches to quantum gravity (loop quantum gravity, causal dynamical triangulations, asymptotic safety) that predict dimensional flow: the spectral dimension of spacetime runs from $\sim 4$ at large scales to $\sim 2$ in the ultraviolet.

**S18: "Gravity on a multifractal" (arXiv:1012.1244, submitted 2010, published 2011).**

This paper introduces the basic framework: field theory on a spacetime equipped with a Lebesgue-Stieltjes measure that encodes dimensional flow. The action is modified by replacing the standard volume form $d^D x$ with a measure $d\varrho(x)$ that depends on a profile function controlling the effective dimension at each scale. Calcagni derives the modified Einstein equations and explores cosmological implications.

The key physical idea is that dimensional flow toward $D_{\text{eff}} \sim 2$ in the UV could tame the ultraviolet divergences of quantum gravity, since Einstein gravity is renormalizable in two dimensions. Whether this mechanism survives quantization is an open question.

**S19: "Geometry and field theory in multi-fractional spacetime" (arXiv:1107.5041, 2011).**

This paper builds explicit field theories on multifractional backgrounds and discusses the connection to renormalization-group-driven dimensional flow. The multifractional framework is distinguished from fractal models by the presence of multiple scale-dependent contributions to the measure, rather than a single fractal dimension.

**S20: "Geometry of fractional spaces" (arXiv:1106.5787, v3 2013).**

This paper provides the mathematical foundations: fractional measures, distances, dimensions, and the precise relationship between "fractional" and "fractal." Calcagni defines Lebesgue-Stieltjes measures that interpolate between integer-dimensional geometries and establishes the geometric structures needed to do calculus—and therefore physics—on fractional spaces.

The three papers form a coherent program: S20 provides the mathematical foundations, S18 builds gravitational theory on those foundations, and S19 extends to general field theory. A reader interested in Calcagni's program should read them in the order S20, S18, S19.

### 4.4 Status Assessment

The fractional mechanics references (S15–S16) rest on solid mathematical ground and connect to experimentally verified phenomena (viscoelastic materials). The fractional gravity and spacetime references (S17–S20) are mathematically consistent frameworks, but experimental verification remains absent. Calcagni's multifractional spacetime makes predictions for the spectral dimension that could, in principle, be tested by quantum gravity phenomenology, but current observational constraints are weak. The reader should maintain a clear distinction between the established mathematics and the speculative physics.

---

## 5. Applications in Quantum Physics

### 5.1 Overview

This section develops fractional quantum mechanics and fractional quantum field theory. The central construction is the fractional Schrödinger equation, derived by replacing Brownian paths in the Feynman path integral with Lévy flights. This generalization introduces the Lévy index $\alpha \in (1, 2]$ as a new quantum parameter. For $\alpha = 2$, standard quantum mechanics is recovered; for $1 < \alpha < 2$, the kinetic term becomes non-local, fundamentally altering quantum dynamics.

The section contains two partly independent research threads: Laskin's fractional quantum mechanics program (S21–S24) and Calcagni's fractional/multifractional quantum field theory (S25–S27). They share the mathematical apparatus of fractional operators but differ in motivation and scope. Laskin begins from the path-integral formulation and asks what quantum mechanics looks like when paths are Lévy flights. Calcagni begins from the spacetime measure and asks what quantum field theory looks like when the spacetime dimension flows.

### 5.2 Laskin's Program: Fractional Quantum Mechanics (S21–S24)

**S21: Laskin (2002).** "Fractional Schrödinger Equation," arXiv:quant-ph/0206098.

This paper introduces the foundational framework. Laskin's starting point is the Feynman path integral, which represents the quantum propagator as a sum over all paths from initial to final position, weighted by $e^{iS/\hbar}$. In standard quantum mechanics, the measure on paths is Wiener measure—the probability measure on Brownian paths. Laskin replaces Wiener measure with the measure on $\alpha$-stable Lévy processes, obtaining the "fractional path integral."

The resulting evolution equation is the fractional Schrödinger equation:

$$i\hbar \frac{\partial \psi}{\partial t} = D_\alpha (-\hbar^2 \Delta)^{\alpha/2} \psi + V\psi$$

where $(-\Delta)^{\alpha/2}$ is the fractional Laplacian (defined in Section 6), $D_\alpha$ is a generalized diffusion coefficient with dimensions $[\text{energy}]^{1-\alpha} \cdot [\text{length}]^\alpha \cdot [\text{time}]^{-\alpha}$, and $\alpha \in (1, 2]$ is the Lévy index. For $\alpha = 2$, this reduces to the standard Schrödinger equation with $D_2 = 1/2m$.

The non-locality of the fractional Laplacian means that the quantum dynamics at a point depends on the wave function throughout space—a radical departure from standard quantum mechanics, where the kinetic energy operator $-\hbar^2 \Delta / 2m$ involves only local derivatives.

**S22–S23: Laskin (2008, 2010).** "Fractional Quantum Mechanics," arXiv:0811.1769; "Principles of Fractional Quantum Mechanics," arXiv:1009.5533.

These review papers consolidate and extend the framework. Key results include:

*Fractional uncertainty relation.* The standard Heisenberg uncertainty principle $\Delta x \cdot \Delta p \geq \hbar/2$ is modified in fractional quantum mechanics. The precise form depends on $\alpha$ and differs from the standard relation in a way that reflects the non-Gaussian character of Lévy processes.

*Fractional hydrogen atom.* The energy levels of the fractional analog of the hydrogen atom—a particle in a Coulomb potential governed by the fractional Schrödinger equation—are computed. The spectrum differs from the Bohr spectrum and depends on $\alpha$.

*Consistency requirements.* The papers establish that the fractional Hamiltonian $H_\alpha = D_\alpha (-\hbar^2 \Delta)^{\alpha/2} + V$ is Hermitian on appropriate function spaces, that probability is conserved, and that the semiclassical limit recovers classical mechanics (in a generalized sense involving Lévy processes rather than Newtonian trajectories).

*Parity and time reversal.* The symmetry properties of the fractional Schrödinger equation under discrete transformations are analyzed. The fractional Laplacian commutes with spatial inversion, preserving parity as a good quantum number.

**S24: Laskin (2018).** *Fractional Quantum Mechanics*, World Scientific.

This monograph consolidates Laskin's program into a comprehensive book-length treatment. It covers the mathematical foundations of Lévy processes, derives the fractional Schrödinger equation from first principles via the path integral, and solves canonical problems: the infinite square well, the harmonic oscillator, and the Coulomb potential in the fractional regime. The book is the definitive reference for Laskin's version of fractional quantum mechanics.

### 5.3 Fractional Quantum Field Theory (S25–S27)

**S25: Calcagni (2010).** "Quantum field theory, gravity and cosmology in a fractal universe," arXiv:1001.0571.

This paper develops a fractional QFT framework built on the Lebesgue-Stieltjes measure approach from Calcagni's spacetime program (Section 4.3). The action for a scalar field $\phi$ on a fractional spacetime takes the form:

$$S = \int d\varrho(x) \left[ \frac{1}{2} \partial_\mu \phi \, \partial^\mu \phi - V(\phi) \right]$$

where $d\varrho(x)$ is the fractional measure encoding dimensional flow. Calcagni derives propagators, develops the perturbative expansion, and investigates renormalization properties. The anomalous dimension of spacetime modifies the UV behavior of loop integrals, with potential implications for the divergence structure.

The paper also treats fermion and gauge fields on fractional spacetimes, though in less detail than the scalar case.

**S26: Calcagni (2017).** "Multifractional theories: an unconventional review," arXiv:1612.05632.

This is an FAQ-style review of the multifractional program, written for an audience that has encountered the basic ideas but has questions about consistency, uniqueness, and observational constraints. The review covers constructions of multifractional derivatives, the symmetries of multifractional spacetimes, and phenomenological constraints from particle physics and cosmology.

A useful feature of this paper is its discussion of the different possible "multifractional" modifications—theories with weighted derivatives, theories with $q$-derivatives, and theories with fractional derivatives—and the physical and mathematical criteria that distinguish among them.

**S27: Calcagni & Rachwał (2023).** "Ultraviolet-complete quantum field theories with fractional operators," arXiv:2210.04914 (posted 2022, journal 2023).

This is the most recent paper in the bibliography and represents a shift in emphasis from Calcagni's earlier work. Rather than modifying the spacetime measure, S27 modifies the kinetic operator: the standard d'Alembertian $\Box$ is replaced by a fractional d'Alembertian $\Box^\alpha$ or a fractional Laplacian in the kinetic term. The paper analyzes different choices of fractional operator, their consequences for renormalizability and unitarity, and the conditions under which fractional modifications can render quantum field theories UV-complete.

This approach is adjacent to but distinct from the "fractal measure" approach of S25. In S25, the non-standard physics enters through the integration measure; in S27, it enters through the differential operator in the action. The two approaches lead to different propagators, different vertex rules, and different UV behavior.

### 5.4 The Conceptual Relationship Between Laskin and Calcagni

Laskin and Calcagni share the mathematical apparatus of fractional operators but differ in scope and ambition. Laskin's program is more conservative: it asks what happens to quantum mechanics when the underlying stochastic process is Lévy rather than Brownian, takes the result as a self-consistent quantum theory with a free parameter $\alpha$, and studies its consequences. The physical interpretation is clear—$\alpha$ characterizes the class of path-integral measures—even if the experimental motivation for $\alpha \neq 2$ in fundamental quantum mechanics is limited.

Calcagni's program is more ambitious and more speculative: it proposes that spacetime itself has a scale-dependent (multi)fractional structure, motivated by hints from quantum gravity, and works out the consequences for field theory. The mathematical framework is more involved, the connection to observation more tenuous, and the internal consistency requirements more demanding.

Both programs remain theoretical proposals without direct experimental confirmation. The distinction between the established mathematics (fractional operators, Lévy processes, path integrals) and the speculative physics (whether nature actually employs fractional structures at fundamental scales) should be kept firmly in mind.

### 5.5 Reading Path for This Section

Begin with Laskin's S21 for the fractional Schrödinger equation, then S22 or S23 for the broader framework. Calcagni's S26 provides the most accessible entry to the multifractional QFT program. S27 can be read independently as a study of fractional operators in QFT.

---

## 6. Core Mathematical Framework

The four application domains surveyed above share a common mathematical infrastructure. This section collects the key definitions, relates the different operator conventions, and identifies the special functions that serve as the "atoms" of fractional calculus.

### 6.1 Fundamental Operators

**Riemann-Liouville fractional integral.** For $\alpha > 0$:

$${}_a I^\alpha_t f(t) = \frac{1}{\Gamma(\alpha)} \int_a^t (t - \tau)^{\alpha - 1} f(\tau) \, d\tau$$

This reduces to $n$-fold integration when $\alpha = n \in \mathbb{N}$. The lower limit $a$ matters: different choices of $a$ produce different operators (and different physics). The choice $a = -\infty$ yields the Weyl integral; $a = 0$ is standard for initial-value problems.

**Riemann-Liouville fractional derivative.** For $\alpha > 0$, with $n = \lceil \alpha \rceil$:

$${}_a D^\alpha_t f(t) = \left(\frac{d}{dt}\right)^n {}_a I^{n-\alpha}_t f(t) = \frac{1}{\Gamma(n-\alpha)} \left(\frac{d}{dt}\right)^n \int_a^t (t - \tau)^{n-\alpha-1} f(\tau) \, d\tau$$

First integrate to make the order an integer, then differentiate. This is the definition developed in Wheeler's S7 and used throughout the mathematical literature.

**Caputo fractional derivative.** For $\alpha > 0$, with $n = \lceil \alpha \rceil$:

$${}^C_a D^\alpha_t f(t) = {}_a I^{n-\alpha}_t \left(\frac{d}{dt}\right)^n f(t) = \frac{1}{\Gamma(n-\alpha)} \int_a^t (t - \tau)^{n-\alpha-1} f^{(n)}(\tau) \, d\tau$$

First differentiate (in the ordinary sense), then integrate. The order of operations is reversed compared to Riemann-Liouville. The practical consequence: the Caputo derivative of a constant is zero (as one would expect), whereas the Riemann-Liouville derivative of a constant is generally nonzero. This makes the Caputo formulation more natural for initial-value problems.

**The relationship between them:**

$${}^C_a D^\alpha_t f(t) = {}_a D^\alpha_t f(t) - \sum_{k=0}^{n-1} \frac{f^{(k)}(a)}{\Gamma(k - \alpha + 1)} (t - a)^{k - \alpha}$$

They agree when $f^{(k)}(a) = 0$ for $k = 0, 1, \ldots, n-1$.

**Grünwald-Letnikov derivative.** The discrete definition:

$$D^\alpha f(x) = \lim_{h \to 0} \frac{1}{h^\alpha} \sum_{k=0}^{\infty} (-1)^k \binom{\alpha}{k} f(x - kh)$$

where $\binom{\alpha}{k} = \frac{\Gamma(\alpha + 1)}{\Gamma(k+1) \Gamma(\alpha - k + 1)}$. This converges to the Riemann-Liouville derivative under appropriate smoothness conditions and is the basis for most finite-difference numerical schemes for fractional derivatives.

### 6.2 The Fractional Laplacian

Central to fractional quantum mechanics and to the connection with Lévy processes is the fractional Laplacian $(-\Delta)^{\alpha/2}$. It admits several equivalent definitions:

**Fourier definition:**

$$\mathcal{F}[(-\Delta)^{\alpha/2} f](\mathbf{k}) = |\mathbf{k}|^\alpha \, \mathcal{F}[f](\mathbf{k})$$

This is the most transparent definition: the fractional Laplacian multiplies each Fourier mode by $|\mathbf{k}|^\alpha$. For $\alpha = 2$, this recovers the standard Laplacian (up to sign).

**Singular integral (Riesz) definition:**

$$(-\Delta)^{\alpha/2} f(\mathbf{x}) = C_{n,\alpha} \, \text{P.V.} \int_{\mathbb{R}^n} \frac{f(\mathbf{x}) - f(\mathbf{y})}{|\mathbf{x} - \mathbf{y}|^{n + \alpha}} \, d\mathbf{y}$$

where $C_{n,\alpha}$ is a normalization constant depending on the spatial dimension $n$ and the order $\alpha$, and P.V. denotes the Cauchy principal value. This definition makes the non-locality explicit: the fractional Laplacian at a point depends on the values of $f$ throughout all of $\mathbb{R}^n$, weighted by a power-law kernel that decays as $|\mathbf{x} - \mathbf{y}|^{-(n+\alpha)}$.

**Probabilistic interpretation:** $(-\Delta)^{\alpha/2}$ is the infinitesimal generator of the semigroup of a symmetric $\alpha$-stable Lévy process. This is the precise mathematical statement connecting Section 2 (Lévy flights) to Section 5 (fractional Schrödinger equation).

### 6.3 Special Functions

**Mittag-Leffler function.** The one-parameter Mittag-Leffler function:

$$E_\alpha(z) = \sum_{k=0}^{\infty} \frac{z^k}{\Gamma(\alpha k + 1)}$$

For $\alpha = 1$, this is the exponential: $E_1(z) = e^z$. For general $\alpha$, it plays the role in fractional calculus that $e^z$ plays in integer-order calculus. Specifically, the solution of the fractional relaxation equation ${}^C D^\alpha_t y(t) = -\lambda y(t)$ with $y(0) = y_0$ is $y(t) = y_0 E_\alpha(-\lambda t^\alpha)$.

The two-parameter generalization:

$$E_{\alpha,\beta}(z) = \sum_{k=0}^{\infty} \frac{z^k}{\Gamma(\alpha k + \beta)}$$

appears in solutions of more general fractional ODEs, analogous to how matrix exponentials and convolution integrals appear in systems of integer-order ODEs.

The Mittag-Leffler function interpolates between exponential decay (for $\alpha = 1$) and algebraic (power-law) decay (for $\alpha \to 0$). This interpolation is the mathematical expression of the "stretched exponential" relaxation observed in viscoelastic materials, dielectric relaxation, and many other physical systems.

**Fox H-function.** The most general solutions to fractional evolution equations involve the Fox H-function, a highly general special function defined via a Mellin-Barnes integral. Most practitioners will encounter it only through its relationship to simpler special functions (Mittag-Leffler, Wright, Meijer G) that arise in specific problems.

---

## 7. Cross-Cutting Themes

### 7.1 Lévy Processes as Unifying Thread

Lévy processes provide the central connecting theme across all four sections of the bibliography. In Section 2, they model anomalous diffusion and financial asset dynamics. In Section 3, their infinitesimal generators give rise to fractional differential operators. In Section 4, fractional calculus on manifolds requires understanding of Lévy-type processes on curved spaces (at least implicitly). In Section 5, Lévy path integrals replace Brownian path integrals to derive fractional quantum mechanics.

This is not a coincidence but a reflection of mathematical structure: $\alpha$-stable Lévy processes are the unique processes that are self-similar, have stationary independent increments, and generalize Brownian motion. Their generators are necessarily fractional powers of the Laplacian, and any physical theory built on such processes will inherit fractional differential equations as its evolution equations.

### 7.2 Non-locality

Fractional operators are inherently non-local: the fractional derivative of a function at a point depends on the function's values throughout a region (for Riemann-Liouville, on the entire interval $[a, x]$; for the fractional Laplacian, on all of $\mathbb{R}^n$). This non-locality appears physically in several guises:

- **Memory effects** in viscoelastic materials: the stress at time $t$ depends on the entire strain history, weighted by a power-law kernel.
- **Non-local interactions** in fractional gravity: the modification of Einstein's equations by fractional operators introduces effective interactions that are not confined to a point.
- **Extended paths** in Lévy flight diffusion: the occasional large jumps that characterize Lévy processes mean that transport at a point depends on the source distribution at distant locations.
- **Non-local kinetic terms** in fractional quantum mechanics: the fractional Laplacian in the Schrödinger equation means that the time evolution of $\psi(\mathbf{x}, t)$ depends on $\psi$ throughout space, not just on local derivatives.

The connection between non-locality and non-integer order is fundamental: it is the power-law kernel $(t - \tau)^{\alpha - 1}$ or $|\mathbf{x} - \mathbf{y}|^{-(n+\alpha)}$ that makes fractional operators non-local, and this kernel is inextricably linked to the non-integer order $\alpha$.

### 7.3 Anomalous Scaling and Dimensional Flow

A recurring theme across the bibliography is the departure from integer-dimensional behavior:

- In stochastic processes (Section 2), the mean-squared displacement scales as $t^{2/\alpha}$ rather than $t$, with $\alpha$ controlling the anomalous exponent.
- In multifractional spacetime (Section 4), the effective dimension itself becomes scale-dependent, interpolating between different values at different scales. Calcagni's program implements this through profile functions in the integration measure.
- In fractional QFT (Section 5), the spectral dimension of spacetime runs with energy, potentially modifying UV behavior. The proposal that $D_{\text{eff}} \to 2$ in the deep UV, if correct, could resolve the non-renormalizability of quantum gravity.

These phenomena are related through the mathematical structure of fractional operators. The scaling exponent $\alpha$ in a Lévy process, the order of the fractional derivative in a differential equation, and the anomalous dimension in a quantum field theory are all manifestations of the same underlying departure from the integer-order, Gaussian, local structure of classical mathematics and physics.

### 7.4 The MSRJD Connection

Although not explicitly developed in the current bibliography, the Martin-Siggia-Rose-Janssen-de Dominicis (MSRJD) formalism provides an important bridge between several themes. The MSRJD formalism rewrites stochastic differential equations as field theories via a path-integral representation. When the underlying stochastic process is Lévy rather than Brownian, the resulting field theory naturally involves fractional operators. This connects the stochastic processes of Section 2, the path integrals of Section 5, and the broader field-theoretic framework of the *Projects in Scientific Computing*.

---

## 8. Critical Assessment and Recommendations

### 8.1 Strengths of the Bibliography

The twenty-seven references assembled here effectively span foundational mathematics through speculative physics applications. Several specific strengths deserve note:

- Wheeler's lecture notes (S7–S10) provide freely accessible, pedagogically excellent entry points to the mathematical foundations. For a physics audience, these are superior to most textbook introductions.
- The financial mathematics references (S2–S4, S6) demonstrate practical applications of Lévy processes that are testable against market data, grounding the more abstract mathematics in empirical reality.
- Laskin's papers and book (S21–S24) provide a coherent, self-contained development of fractional quantum mechanics.
- Calcagni's systematic program (S18–S20, S25–S27) represents a serious attempt to extend fractional ideas to spacetime geometry and quantum field theory, with clear mathematical development even where the physics remains speculative.

### 8.2 Limitations and Gaps

The bibliography is explicitly labeled as a draft, and several notable topics are absent:

- **The Caputo derivative** is mentioned in several textbooks but does not receive dedicated treatment proportional to its importance, particularly for applied problems.
- **Fractional Brownian motion** is absent. While distinct from Lévy processes (it is Gaussian, with long-range dependence rather than heavy tails), it is a major application of fractional calculus in its own right.
- **Applications in control theory and signal processing**, which represent some of the most developed engineering applications of fractional calculus, are covered only through the general textbooks.
- **Experimental and observational constraints** on fractional theories in physics are not systematically reviewed. For the speculative gravity and QFT proposals, this is a significant omission.
- A **glossary of operator conventions**—clarifying the relationships among Riemann-Liouville, Caputo, Grünwald-Letnikov, Marchaud, Weyl, and spectral definitions—would substantially improve navigability.

### 8.3 Status of Theoretical Proposals

The references in this bibliography range from established, textbook-level mathematics to speculative theoretical physics. A rough classification:

**Established results:**
- Riemann-Liouville and Caputo fractional calculus (mathematical foundations, Sections 3 and 6)
- Lévy processes and their generators (Section 2)
- Fractional viscoelasticity (Section 4, S16)
- The mathematical structure of the fractional Schrödinger equation (Section 5, S21–S24)—the mathematics is rigorous; whether it describes nature is a separate question

**Plausible extensions under active investigation:**
- Fractional Lagrangian and Hamiltonian mechanics (S15)—mathematically consistent, with potential applications to non-conservative systems
- Dimensional flow in quantum gravity (S18–S20)—motivated by independent quantum gravity programs, but lacking direct experimental confirmation

**Speculative proposals requiring further scrutiny:**
- Fractional modifications of GR (S17)—mathematically possible but physically motivated primarily by formal analogy
- Fractional QFT as a route to UV completion (S27)—an interesting technical proposal whose physical relevance depends on whether nature employs fractional structures at fundamental scales


---

## 9. Conclusion and Future Directions

The fractional calculus bibliography provides a curated entry point into a mathematically rich and physically consequential field. The twenty-seven references trace a coherent arc from eighteenth-century mathematical curiosities through modern applications in finance, materials science, and theoretical physics. The central role of Lévy processes in connecting these diverse applications is the organizing thesis, and it holds up well under scrutiny.

For a reader with graduate-level training in mathematics and physics, the recommended reading path proceeds as follows: Wheeler's notes (S7, S9) for foundational constructions and the fractional Laplacian; Kilbas (S11) as a reference for precise operator identities; the Lévy process literature (S1, S3, S5) for stochastic motivation; Laskin (S21–S23) for fractional quantum mechanics; and Calcagni (S26, S20) for the multifractional spacetime program. The financial applications (S2–S4) and numerical methods (S6, S14) are consulted as dictated by the reader's specific interests.

The bibliography as it stands is weighted toward the physics of fractional operators and underweights their engineering and applied-mathematics applications. Expanding the coverage to include fractional control theory, fractional signal processing, and experimental constraints on fractional physical theories would strengthen the collection. The bridge to biophysics—where power-law relaxation, anomalous diffusion in cellular environments, and viscoelastic models of tissue mechanics all involve fractional operators—represents a natural extension given the broader context of the *Projects in Scientific Computing*.

---

## Appendix A: Operator Conventions Quick Reference

| Operator | Definition | Domain | Notes |
|----------|-----------|--------|-------|
| Riemann-Liouville integral ${}_a I^\alpha_t$ | $\frac{1}{\Gamma(\alpha)} \int_a^t (t-\tau)^{\alpha-1} f(\tau) d\tau$ | $\alpha > 0$ | Reduces to $n$-fold integration for $\alpha = n$ |
| Riemann-Liouville derivative ${}_a D^\alpha_t$ | $(d/dt)^n \, {}_a I^{n-\alpha}_t f$ | $n = \lceil \alpha \rceil$ | Integrate first, then differentiate |
| Caputo derivative ${}^C_a D^\alpha_t$ | ${}_a I^{n-\alpha}_t (d/dt)^n f$ | $n = \lceil \alpha \rceil$ | Differentiate first, then integrate |
| Fractional Laplacian $(-\Delta)^{\alpha/2}$ | $\mathcal{F}^{-1}[|\mathbf{k}|^\alpha \hat{f}]$ | $0 < \alpha < 2$ | Generator of $\alpha$-stable Lévy process |
| Grünwald-Letnikov $D^\alpha$ | $\lim_{h\to 0} h^{-\alpha} \sum (-1)^k \binom{\alpha}{k} f(x-kh)$ | $\alpha > 0$ | Basis for numerical discretization |

**Key identity:** ${}^C_a D^\alpha_t f = {}_a D^\alpha_t f - \sum_{k=0}^{n-1} \frac{f^{(k)}(a)}{\Gamma(k-\alpha+1)}(t-a)^{k-\alpha}$

**Caputo vs. Riemann-Liouville for initial-value problems:** Caputo is preferred because ${}^C D^\alpha_t (\text{const}) = 0$ and initial conditions take the familiar form $f(0) = f_0$, $f'(0) = f_1$, etc.

---

## Appendix B: Notation

| Symbol | Meaning |
|--------|---------|
| $\alpha$ | Lévy stability index / fractional order, typically $\alpha \in (0, 2]$ |
| $\Gamma(\cdot)$ | Euler's Gamma function |
| $E_\alpha(z)$ | One-parameter Mittag-Leffler function |
| $E_{\alpha,\beta}(z)$ | Two-parameter Mittag-Leffler function |
| $(-\Delta)^{\alpha/2}$ | Fractional Laplacian |
| $D_\alpha$ | Generalized diffusion coefficient (fractional QM) |
| $d\varrho(x)$ | Lebesgue-Stieltjes measure (multifractional spacetime) |
| $\Box$ | d'Alembertian operator |
| P.V. | Cauchy principal value |


**Bibliography**

### 1. L’evy Flights

| ID  | Link                                                                                                                                                        | Notes                                                                                                        |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| S1  | [Bouchaud & Georges *"Anomalous Diffusion in Disordered Media"* 1990](https://www.sciencedirect.com/science/article/abs/pii/037015739090099N)              | Comprehensive review of anomalous diffusion phenomena in disordered systems, focusing on Lévy flight processes. |
| S2  | [Duffie et al *"SVJJ"* 2000](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=157733)                                                                 | Introduces the SVJJ model combining stochastic volatility with double‐jump processes for asset returns.       |
| S3  | [Carr et al *"SV for L’evy"* 2003](https://engineering.nyu.edu/sites/default/files/2019-03/Carr-stochastic-volatility-levy-processes.pdf)               | Develops stochastic volatility frameworks driven by Lévy processes for option valuation.                      |
| S4  | [Carr and Wu *"Time Changed L’evy Processes"* 2005](https://engineering.nyu.edu/sites/default/files/2019-03/Carr-time-changed-levy-processes-option-pricing.pdf) | Presents option‐pricing methods based on time‐changed Lévy processes to capture stochastic volatility and jumps. |
| S5  | [Chechkin et al *"Introduction to L’evy Flights"* 2008](https://onlinelibrary.wiley.com/doi/10.1002/9783527622979.ch5)                                  | Offers an accessible introduction to Lévy flights and their applications in physics and complex systems.       |
| S6  | [Platen and Bruti Liberati *"Numerical Solution of Jump Diffusions"* 2017](https://link.springer.com/book/10.1007/978-3-642-13694-8)                         | Details numerical techniques for simulating and solving jump‐diffusion models in quantitative finance.         |

---

### 2. Fractional Calculus

| ID  | Link                                                                                                                                                         | Notes                                                                                                                       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| S7  | [N. A. Wheeler *"Fractional Calculus I"* 1997](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Fractional%20Calculus/A.%20Fractional%20Calculus.pdf)         | Covers foundational concepts and definitions in fractional calculus, including historical context and basic operators.     |
| S8  | [N. A. Wheeler *"Fractional Calculus II"* 1997](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Fractional%20Calculus/B.%20Fractional%20Leibniz.pdf)       | Explores the fractional Leibniz rule and related differentiation techniques.                                                |
| S9  | [N. A. Wheeler *"Fractional Calculus III"* 1998](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Fractional%20Calculus/C.%20Fractional%20Laplacian.pdf)      | Discusses the fractional Laplacian operator and its mathematical properties.                                               |
| S10 | [N. A. Wheeler *"Fractional Calculus IV"* 2005](https://www.reed.edu/physics/faculty/wheeler/documents/Miscellaneous%20Math/Fractional%20Calculus/D.%20Alternative%20Approach.pdf)       | Proposes alternative approaches to fractional differentiation and integration.                                             |
| S11 | [Kilbas et al *"Fractional Differential Equations"* 2006](https://shop.elsevier.com/books/theory-and-applications-of-fractional-differential-equations/kilbas/978-0-444-51832-3)    | Presents theory and applications of fractional differential equations in various scientific contexts.                       |
| S12 | [Sabatier et al *"Advances in Fractional Calculus"* 2007](https://link.springer.com/book/10.1007/978-1-4020-6042-7)                                            | Compiles recent developments and applications in fractional calculus across multiple disciplines.                           |
| S13 | [Zhou et al *"Fractional Differential Equations"* 2016](https://www.worldscientific.com/worldscibooks/10.1142/10238?srsltid=AfmBOoqtFxgTRF5fAIw9HjWv_DqnWxQLyvX96Vt4DHlVBQd99dWt9F9h#t=aboutBook) | Provides advanced methods for solving fractional differential equations with illustrative application examples.             |
| S14 | [Baleanu et al *"Fractional Calculus: Numerical Methods"* 2017](https://www.worldscientific.com/worldscibooks/10.1142/10044?srsltid=AfmBOoq4OKEbRsW_-ZlM-y49cqSCYjsqdJMyxqhKXprFBB9wRxI7vZGS#t=aboutBook) | Focuses on numerical algorithms for approximating fractional‐order operators and solving related equations.                  |

---

### 3. Applications: Classical Physics

| ID   | Link                                                                                                                                                          | Notes                                                                                                          |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| S15  | [Cresson *"Fractional Lagrangian Mechanics"* 2006](https://arxiv.org/abs/math/0605752)                                                                        | Develops a fractional calculus extension of Lagrangian mechanics for systems with non-integer dynamics.       |
| S16  | [Atanakčović et al *"Fractional Mechanics"* 2004](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118577530)                                         | Offers a comprehensive treatise on mechanics formulated using fractional derivatives and applications in physics. |
| S17  | [Vacaru *"Fractional Blackholes"* 2010](https://arxiv.org/abs/1004.0628)                                                                                   | Investigates black hole solutions within fractional spacetime frameworks and modified gravity theories.                    |
| S18  | [Calcagni *"Fractional Gravity"* 2011](https://arxiv.org/abs/1012.1244)                                                                                     | Introduces a fractional-dimensional approach to gravity and explores its cosmological implications.                         |
| S19  | [Calcagni *"Multi-fractal Spacetime"* 2011](https://arxiv.org/abs/1107.5041)                                                                                | Studies multifractional spacetime models featuring scale-dependent dimensions and varying physical constants.             |
| S20  | [Calcagni *"Geometry of Fractional Spaces"* 2013](https://arxiv.org/abs/1106.5787)                                                                          | Examines the geometric structures and measures that underpin fractional spaces and their implications for field theories. |

---

### 4. Applications: Quantum Physics

| ID   | Link                                                                                                                                                         | Notes                                                                                                            |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| S21  | [Laskin *"Fractional Schrödinger"* 2002](https://arxiv.org/abs/quant-ph/0206098)                                                                             | Proposes the fractional Schrödinger equation as a generalization of quantum mechanics using Lévy path integrals. |
| S22  | [Laskin *"Fractional Quantum Mechanics"* 2008](https://arxiv.org/abs/0811.1769)                                                                              | Reviews theoretical foundations and key applications of fractional quantum mechanics in diverse systems.          |
| S25  | [Calcagni *"Fractional Quantum Field Theory"* 2010](https://arxiv.org/abs/1001.0571)                                                                                           | Develops a fractional quantum field theory framework incorporating anomalous dimension effects and scale-dependent operators.                 |
| S23  | [Laskin *"Principles of Fractional Quantum Mechanics"* 2010](https://arxiv.org/abs/1009.5533)                                                                 | Presents fundamental principles and physical interpretations of quantum systems governed by fractional dynamics.  |
| S26  | [Calcagni *"Multifractional Quantum Fields"* 2017](https://arxiv.org/abs/1612.05632)                                                                                   | Explores multifractional quantum field theories that exhibit scale-dependent structures and varying fractal dimensions.                        |
| S24  | [Laskin *"Fractional Quantum Mechanics"* 2018](https://www.worldscientific.com/worldscibooks/10.1142/10541?srsltid=AfmBOorHlSAIZl1IG99KxgusItDvYNowyJjzpje7lHRyTFQisvVxYvKN#t=aboutBook)   | Compiles advanced topics and recent research methodologies in fractional quantum mechanics.                       |
| S27  | [Calcagni *"Quantum Fields Fractional Operators"* 2023](https://arxiv.org/abs/2210.04914)                                                                     | Analyzes the role of fractional differential operators in shaping the behavior and renormalization properties of quantum fields.               |
