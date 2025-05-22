---
layout:   post
title: "Stochastic Quantization"
date: 2025-05-03 10:00:00 +0800
categories: [Stochastic Quantization]
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


In this notation, the background spacetime is $x^{a} = (t,x^{i})$ with $n-1$ spatial dimensions,  and the index $\mathfrak{k}$ indicates internal symmetries.  Let $s$ be the affine parameter (proper time) along a world line and let $\xi^{\mathfrak{k}}(s,x^{d})$ be a vector of general noise indexed over the internal symmetry.  The stochastic partial differential equation of stochastic quantization is

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
- $\nabla_{a} \equiv \partial_{a} - \mathcal{A}_{a}$ is the covariant derivative of the connection,
- $\mathcal{A}_{b}$ is a connection field of a gauge-symmetry fibre bundle $\mathcal{E}$ over $\mathcal{M}$,
- $\mathfrak{g}_{\mathfrak{j}\mathfrak{k}}$ governs the trace over the internal symmetry, and
- $U(\Phi^{\mathfrak{j}})$ is a generalized potential governing dynamics and self-interactions.

This example is sufficient to study effects of:

1. The background spacetime geometry (base manifold dimension, topology, curvature, etc),
2. The gauged internal symmetry,
3. The parameter-space survey of the dynamical system (stationary states, instabilities, symmetry breaking, etc).



For example, in the limit of zero spatial dimensions ($n=1$), quantum mechanics is formulated as the following stochastic PDE:

$$
\frac{\partial}{\partial s}\,x^{\mathfrak{i}}(s,t) = -\,\frac{\delta}{\delta x^{\mathfrak{i}}}\,S\bigl[x^{\mathfrak{j}}(s,t)\bigr] + \xi^{\mathfrak{i}}(s,t),
$$

where 

$$
S[x^{\mathfrak{l}}] = \int dt'\;\bigl\{\mathfrak{g}_{\mathfrak{i}\mathfrak{j}} \dot{x}^{\mathfrak{i}}\dot{x}^{\mathfrak{j}} + A_{\mathfrak{k}}\,\dot{x}^{\mathfrak{k}} - U(x^{\mathfrak{l}})\bigr\}.
$$

[Here $\dot{x}^{\mathfrak{i}} \equiv \frac{d }{dt} x^{\mathfrak{i}}(t)$ with $t$ denoting 'clock on the wall' Newtonian time.]

This generic formalism applies to study of:

- Foundations of quantum mechanics,
- Path integration,
- Non-equilibrium statistical mechanics.

More specifically, this approach permits numerical analysis of:

- The effective action functional and functional renormalization group,
- The path integral of the non-relativistic particle on a curved spacetime,
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

## References

1. First Reference TBD
2. Second Reference TBD