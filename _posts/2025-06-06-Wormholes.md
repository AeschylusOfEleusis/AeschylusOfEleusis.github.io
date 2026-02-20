---
layout:   post
title: "Worm holes"
date: 2025-06-06 10:00:00 +0800
categories: [Numerical Relativity]
tags: [Numerical Relativity, Quantum Field Theory, Black holes, Worm holes, Scientific Computing]
math:       true        # enable KaTeX
---
# Notes on Rotating Lorentzian Worm holes (Draft)

## Abstract

Notes are provided concerning rotating wormholes in General Relativity.  Since Teo's original 1998 article, almost 3 decades of research established an active area with open problems: 1. The rotational symmetry of the spacetime poses exact, perturbative and numerical challenges, and 2. The novel topology requires, consistently with global theorems, source matter violating conventional energy conditions. [Proposals for exotic source matter historically include quantum fields and phantom scalar fields; e.g., Ellis's original 1973 article.] Most recently, wormhole solutions of the Einstein Maxwell Dirac system were found and explored numerically to demonstrate instability to gravitational collapse. The following notes are divided into sections supporting research; including primary literature concerning axisymmetry, spin 1/2 Dirac fields in curved spacetimes, and gravitational lensing.     

## Introduction

The subject of rotating traversable wormholes in general relativity sits at an intersection of exact-solution theory, numerical relativity, spinor field theory, and gravitational-wave phenomenology. From that position the subject naturally motivates projects in scientific computing. The treatment here is bibliographic; with aim to provide a structured reading path through the literature: From Ellis's 1973 drainhole through recent numerical studies of dynamical stability. The 46 primary references catalogued are organized by five thematic blocks, each building on the preceding material and each connected to concrete computational projects.

A traversable Lorentzian wormhole is, at minimum, a horizon-free spacetime geometry connecting two asymptotic regions through a throat---a minimal-area two-surface on an appropriate spatial slice. The "traversable" qualifier, in the sense of Morris and Thorne (1988), demands that a physical observer can pass through the throat in finite proper time without encountering singularities, horizons, or lethal tidal forces. This is a stringent requirement. In classical general relativity, it generically forces violation of the null energy condition (NEC) at or near the throat, which means the matter threading the geometry must have properties that no known classical field possesses.

Rotation further complicates the picture in ways that are both technically demanding and physically illuminating. A stationary, axially symmetric wormhole carries nonzero $g_{t\phi}$---frame dragging---and this introduces ergoregions, superradiant scattering channels, axis-regularity constraints, and nontrivial topology in the space of allowed solutions. A recurring lesson across the literature surveyed here is that "rotating" a static wormhole is far from straightforward: naive solution-generating techniques can introduce ring singularities, string defects, non-smooth throats, or violations of asymptotic flatness. Getting the rotation right requires either careful perturbative expansions (slow-rotation approximations) or full numerical construction of nonlinear solutions.

The literature on wormholes is vast and uneven: All of it is speculative, and the boundary between serious theoretical physics and science fiction is not always well-marked. The references considered here were chosen with an emphasis on mathematical rigor, computational tractability, and physical relevance: Teo-style stationary axisymmetric wormhole ansätze, the modern "black-bounce" interpolation program connecting regular black holes to traversable wormholes, and the Einstein-Dirac-Maxwell construction that avoids phantom fields. 

The notes are organized as follows. Sections one through three develop the core: Foundational solutions, the taxonomy of rotating geometries, and the modern interpolation program connecting regular black holes to traversable wormholes. Following sections treat the Einstein-Dirac-Maxwell (EDM) wormhole program, which represents the most significant recent theoretical development in the field---and whose dynamical viability remains an open question; energy conditions and the constraints they impose on traversability; the mathematical infrastructure of axisymmetric spacetimes needed for numerical work; Dirac fields in curved spacetime, which supply both the matter models and the technical machinery for the EDM program; and gravitational lensing and observational signatures. The final sections collect open problems and directions for computational projects, followed by an annotated bibliography providing per-reference commentary aligned to the original research page.

Nb. Here the metric signature is $(-,+,+,+)$, with geometrized units $G = c = 1$, and the standard Einstein field equations $G_{\mu\nu} = 8\pi T_{\mu\nu}$. The null energy condition (NEC) states that $T_{\mu\nu} k^\mu k^\nu \geq 0$ for all null vectors $k^\mu$. NEC "violation," means that there exists at least one null vector for which this inequality reverses---a necessary condition, in classical GR, for the existence of a traversable throat


## Definitions and Conventions

Before proceeding, a few definitions that are used throughout and that the literature sometimes treats casually.

A *throat* is a minimal-area two-surface on an appropriate spatial slice of the spacetime. More precisely, for a spherically symmetric or axisymmetric wormhole, the throat is the surface where the areal radius achieves its minimum. The *flare-out condition*---that the embedding surface opens outward from the throat---is the geometric statement that the second derivative of the areal radius satisfies a particular inequality, and it is this condition that, via the Einstein equations, forces NEC violation for the threading matter.

*Traversable* means, following Morris and Thorne (1988), that a physical observer (timelike worldline) can pass from one asymptotic region to the other in finite proper time without encountering singularities, horizons, or tidal forces exceeding some specified tolerance. This is an operational definition, and it is important to distinguish it from *mathematical* traversability (the existence of complete geodesics connecting both sides), which does not account for the physical survival of the traveler.

*Dynamical traversability* is a stronger condition: the wormhole must remain traversable when perturbed from exact stationarity. As Kain's results demonstrate, a geometry that is traversable in the static sense can fail to be traversable in the dynamical sense if perturbations cause horizon formation.

The *Teo metric* refers to the general stationary, axially symmetric wormhole ansatz introduced by Teo (1998), parameterized by four functions of $r$ and $\theta$. The *Papapetrou form* of a stationary, axisymmetric metric is a closely related parameterization used in the exact-solutions literature (Stephani et al. 2003). The two are not identical, and translations between them require care with coordinate choices and conformal factors.


## Foundational Solutions

### The Ellis-Bronnikov Drainhole

The story begins with Ellis (1973), who constructed the first traversable wormhole geometry---though the terminology did not yet exist. The Ellis drainhole (independently discovered by Bronnikov) is supported by a phantom scalar field: a scalar with reversed kinetic-term polarity, so that the stress-energy tensor violates the NEC. The resulting spacetime is geodesically complete, horizonless, and connects two asymptotically flat regions. In the simplest symmetric case the geometry is often treated as massless, while more general asymmetric members of the family can carry different ADM masses as seen from the two sides, with "attractive" behavior on one side and "repulsive" on the other. The model is important less as a physically realistic proposal than as a clean demonstration of what NEC violation buys: a smooth, traversable bridge between two otherwise disconnected regions of spacetime.

The Ellis-Bronnikov solution remains the standard test case for computational work. Its analytic simplicity makes it the natural starting point for perturbation theory, numerical evolution, and ray-tracing studies. Nearly every subsequent development in the field can be understood as an attempt to generalize, stabilize, or replace this archetype.

The reader should note that "phantom scalar" and "ghost scalar" are used interchangeably in the literature to denote a scalar field with wrong-sign kinetic energy: $\mathcal{L} = +\frac{1}{2} \nabla_\mu \phi \nabla^\mu \phi$ rather than the standard $-\frac{1}{2} \nabla_\mu \phi \nabla^\mu \phi$. This sign flip is precisely what produces the NEC-violating stress-energy needed for a traversable throat. The physical objection is immediate: a wrong-sign kinetic term implies that the field's energy is unbounded below, leading to instabilities in the quantum theory. Whether this objection is fatal depends on whether one regards the phantom scalar as a fundamental field or as an effective description of some more fundamental physics (such as quantum vacuum effects).

### The Modern Framework: Visser (1996)

Visser's monograph *Lorentzian Wormholes: From Einstein to Hawking* established the conceptual and mathematical framework that the field still uses. The book systematizes the discussion of wormhole kinematics (the flare-out condition for the throat), energy condition violations (pointwise and averaged), thin-shell constructions ("cut-and-paste" methods using the Israel junction conditions), chronology protection, and quantum/semiclassical mechanisms---Casimir-type effects, vacuum polarization---that might supply the needed NEC violation. Chapters on topological censorship connect directly to the "no-go" statements that any serious wormhole proposal must confront.

For the reader approaching this literature for the first time, Visser's book remains the single best entry point. It is pedagogically organized, mathematically rigorous without being impenetrable, and honest about the difference between what is established and what is speculative.

### The Teo Ansatz: Rotating Traversable Wormholes

Teo (1998) is the hub reference for the rotating case. The paper introduces a general stationary, axially symmetric wormhole metric ansatz:

$$ds^2 = -N^2 dt^2 + \frac{dr^2}{1 - b(r)/r} + K^2 r^2 \left[ d\theta^2 + \sin^2\theta \left( d\phi - \omega \, dt \right)^2 \right]$$

where $N$, $b$, $K$, and $\omega$ are functions of both $r$ and $\theta$. This separates the geometric structure of the wormhole---encoded in the shape function $b(r)$, redshift function $N$, and conformal factor $K$---from the choice of matter source. The frame-dragging angular velocity $\omega$ captures rotation.

Teo's key findings include: (i) NEC violation is generic at the throat but can be localized to a region around it, with classes of geodesics that traverse the wormhole without encountering exotic matter; (ii) ergoregions can form around the throat, analogous to the ergosphere of Kerr spacetime; and (iii) the metric is sufficiently general to parameterize a wide family of rotating wormholes while remaining tractable for geodesic analysis.

The Teo ansatz functions in the rotating-wormhole literature much as the Kerr metric functions in black hole physics: it provides a geometry-first framework that organizes subsequent work, whether that work involves specific matter models, perturbation theory, or numerical construction.

The physical content of each metric function is worth unpacking. The redshift function $N$ controls gravitational time dilation and must remain finite and nonzero everywhere for the geometry to be horizonless and free of curvature singularities. The shape function $b(r)$ encodes the wormhole's throat geometry: the condition $b(r_0) = r_0$ defines the throat radius, and the flare-out condition $b'(r_0) < 1$ ensures that the embedding surface opens outward from the throat. The conformal factor $K$ allows for angular deformation of the two-spheres. The frame-dragging angular velocity $\omega$ is the new element in the rotating case: it couples the azimuthal and temporal coordinates and vanishes in the static limit.

The Einstein field equations, applied to this ansatz, yield a system of coupled partial differential equations for these four functions sourced by the stress-energy tensor. In general, the system is not analytically solvable; one must either specialize to particular matter models, impose additional symmetry, or resort to numerical methods. The beauty of the Teo approach is that it defers the choice of matter model: one can first study the geometric and geodesic properties of the ansatz for generic function choices, and then impose the field equations as a constraint when a specific matter model is selected.


## Rotating Solutions and Their Construction

### Slow-Rotation Approximations

The most analytically tractable approach to rotating wormholes is the slow-rotation expansion. Kashargin and Sushkov (2008) developed this for wormholes supported by phantom scalar fields, treating the rotation perturbatively to first order in angular momentum. The expansion clarifies which metric functions control frame-dragging effects and how the stress-energy tensor is modified by rotation. For readers familiar with the Hartle-Thorne slow-rotation formalism for neutron stars, the structure is similar: one solves a system of ordinary differential equations for the frame-dragging potential, sourced by the angular momentum density of the supporting matter.

The slow-rotation approach has obvious limitations---it cannot capture ergoregion formation or other strongly nonlinear rotational effects---but it provides essential diagnostic information and analytic benchmarks for numerical codes.

### Fully Nonlinear Numerical Solutions

Kleihaus and Kunz (2014) constructed the first fully nonlinear rotating Ellis wormholes by solving the coupled Einstein-phantom-scalar field equations numerically. These solutions form a continuous family parameterized by angular momentum and throat size, and the numerical construction addresses regularity at the symmetry axis and the domain of existence in parameter space. The work demonstrates that smooth rotation *is* achievable in the Ellis-Bronnikov family, but the solutions require careful treatment of boundary conditions at the throat and at spatial infinity.

Other numerical constructions extend this program. Chew et al. (2019) studied rotating wormholes supported by complex phantom scalar fields, exploring broader parameter regimes and possible observational proxies. Dzhunushaliev et al. (2014) constructed boson-star-like configurations with wormhole cores---objects where additional bosonic matter "dresses" the throat and changes global properties such as mass, angular momentum, and stability.

### Electrovac and NUT-Type Constructions

An alternative route to rotating wormholes works within Einstein-Maxwell theory. Clément and Gal'tsov (2023) constructed rotating traversable wormholes using overcharged Kerr-Newman-NUT solutions, identifying the exotic matter as counter-rotating tensionless Misner-Dirac strings. This approach leverages the solution-generating machinery of stationary axisymmetric electrovac spacetimes---the Ernst equations and related techniques catalogued in Stephani et al. (2003)---but the physical interpretation of the resulting matter content is debatable.

Gibbons and Volkov (2017) examined the zero-mass limit of the Kerr metric and interpreted it as a wormhole, highlighting the subtleties of ring singularities and global causal structure that arise in rotating spacetimes. Volkov (2021) further developed stationary generalizations of the Bronnikov-Ellis wormhole and constructed vacuum ring-wormhole structures, illustrating the richness---and the pathology risks---of the rotating solution space.

A general lesson from this body of work: the space of stationary, axisymmetric wormhole solutions is far larger than naive expectations suggest, but the physically acceptable subset (smooth, asymptotically flat, with interpretable matter content) is considerably smaller.

### Multi-Mouth Wormholes

Emparan et al. (2020) extended the topology beyond simple two-mouth bridges by constructing wormholes with multiple asymptotic regions connected through a common throat network. These multi-mouth solutions raise qualitatively new questions about causal structure, topology change, and the distribution of exotic matter across multiple throats. They remain largely unexplored computationally.


## The Black-Bounce Interpolation Program

One of the most productive developments in recent wormhole physics is the "black-bounce" interpolation framework introduced by Simpson and Visser (2019). The key idea is a one-parameter family of metrics that smoothly interpolates between a traversable wormhole and a regular black hole:

$$ds^2 = -\left(1 - \frac{2m}{\sqrt{r^2 + a^2}}\right) dt^2 + \frac{dr^2}{1 - \frac{2m}{\sqrt{r^2 + a^2}}} + (r^2 + a^2) \, d\Omega^2$$

The parameter $a$ controls the interpolation: for $a > 2m$ the geometry is a traversable wormhole; at $a = 2m$ one obtains an extremal null-bounce (a one-way traversable configuration); for $a < 2m$ the spacetime describes a regular black hole with a spacelike bounce replacing the classical singularity.

This framework is valuable for several reasons. First, it provides a unified setting for comparing observables---shadows, quasinormal modes (QNMs), lensing signatures, gravitational-wave echoes---across the black hole/wormhole divide. Second, the analytic tractability of the metric makes it a practical testbed for computational projects. Third, the interpolation illuminates a conceptual point: from the perspective of the metric, the distinction between a black hole and a wormhole can be a matter of parameters rather than topology.

Subsequent work has extended the black-bounce idea in several directions. Huang and Yang (2019) generalized to charged settings, exploring how electromagnetic charge modifies the horizon/throat structure. Simpson (2021) systematized the parameterization space and clarified the physical interpretation of intermediate configurations. Mazza, Franzin, and Liberati (2021) examined rotating horizonless compact objects in this family, directly relevant to the question of whether wormholes can mimic rotating black holes in astrophysical observations.

Churilova et al. (2021) studied QNMs, echoes, and shadows for wormholes in this class, emphasizing an important practical point: the observational signatures of near-extremal wormholes can be degenerate with those of near-extremal Reissner-Nordström or Kerr black holes. Distinguishing wormholes from black holes may require either very high-precision observations or qualitatively different probes (such as gravitational-wave echoes from reflections at the throat).


## Einstein-Dirac-Maxwell Wormholes

### The EDM Program

The Einstein-Dirac-Maxwell (EDM) wormhole program represents the most significant recent theoretical development catalogued in these notes. The motivating question is whether traversable wormholes can be constructed in general relativity without introducing phantom scalar fields---that is, without explicitly wrong-sign kinetic terms.

Blázquez-Salcedo, Knoll, and Radu (2020, 2021) showed that the answer is conditionally affirmative. They constructed asymptotically flat, traversable wormhole solutions using two massive fermions in a singlet state coupled to Einstein-Maxwell theory. The solutions satisfy a generalized Smarr relation connecting them to extremal Reissner-Nordström black holes, with the charge-to-mass ratio exceeding unity ($Q_e / M > 1$).

A careful distinction is needed here, and it is one the literature sometimes obscures. "Without phantom matter" does not mean "without NEC violation." The spinor stress-energy tensor in these solutions *does* violate the NEC at the throat---this is unavoidable for traversability in classical GR. What the EDM construction avoids is the introduction of a scalar field with explicitly wrong-sign kinetic energy. The NEC violation is instead sourced by the classical Dirac field's stress-energy, which can have the appropriate sign structure in certain configurations. Whether this represents a genuine physical improvement over phantom scalars is a matter of ongoing debate.

The original symmetric EDM solutions require a junction condition at the throat with a discontinuous fermionic charge density. Bronnikov et al. (2021) criticized this as potentially unphysical. Konoplya and Zhidenko (2021, 2022) responded by constructing asymmetric EDM wormholes with smooth matter fields, avoiding the junction condition issues of the symmetric case but introducing other technical complications.

### Dynamical Viability: Kain's Numerical Relativity Results

The critical test for any wormhole solution is dynamical: does the geometry survive when perturbed, or does it collapse? Kain (2023) performed numerical relativity evolutions of EDM wormhole initial data and obtained a definitive negative result. In all cases studied, black holes form that are connected by the wormhole throat---but the throat becomes non-traversable, trapped behind horizons. Null geodesics that nominally traverse the throat become trapped inside black hole horizons before reaching the other side.

This result does not invalidate the EDM solutions as mathematical constructions, but it severely undermines their physical relevance as models of traversable wormholes. The instability appears generic: it is not an artifact of particular parameter choices or initial perturbations. The lesson is consistent with a broader pattern in wormhole physics---static traversable solutions are generically dynamically unstable.

Kain (2023) also reformulated the EDM wormhole construction within semiclassical gravity, treating the Dirac field quantum mechanically and sourcing the Einstein equations with the expectation value of the stress-energy tensor. This places the construction on somewhat firmer theoretical footing and extends the solution space, but does not resolve the stability problem.

### Implications

The EDM program illustrates a general tension in wormhole physics: the ease of constructing static solutions versus the difficulty of making them dynamically viable. For computational projects, the EDM system offers rich opportunities---the coupled Einstein-Dirac-Maxwell equations provide a nontrivial test case for numerical relativity codes, and the stability analysis involves techniques (constraint-preserving evolution, apparent horizon finding, geodesic tracing in dynamical spacetimes) that are broadly applicable.


## Energy Conditions and Traversability Constraints

The energy conditions provide the theoretical constraints that any traversable wormhole must navigate. Two references in the catalog are pivotal.

### Minimizing Exotic Matter: Visser, Kar, and Dadhich (2003)

Visser, Kar, and Dadhich demonstrated that traversable wormholes can be constructed with arbitrarily small *total* exotic matter content. They introduced the volume integral quantifier

$$I_V = \int (\rho + p_r) \, dV$$

and showed that for suitably chosen shape functions, $\vert I_V \vert$ can be made arbitrarily small while maintaining traversability. The key insight is that while the NEC must be violated *locally* at the throat (this is a geometric theorem, following from the flare-out condition), the *integrated* amount of violation can be minimized through careful engineering of the wormhole geometry.

This is an important result for assessing the physical plausibility of wormholes: it means the "cost" in exotic matter is not fixed by the topology but can in principle be reduced. However, it does not eliminate the need for NEC violation entirely---that remains an inescapable consequence of traversability in classical GR.

### The Achronal Averaged Null Energy Condition: Wall (2010)

Wall proved a version of the averaged null energy condition (ANEC) for achronal complete null geodesics (null lines), deriving it from the generalized second law of black hole thermodynamics. The standard ANEC states

$$\int T_{\mu\nu} k^\mu k^\nu \, d\lambda \geq 0$$

along complete null geodesics, and Wall's achronal version applies to null geodesics that do not intersect their own chronological past or future.

This result is typically read as *strengthening* topological censorship and *ruling out* traversable wormholes within its domain of applicability. The reasoning is: a null geodesic traversing a wormhole throat would violate the achronal ANEC, and Wall's theorem (under its assumptions, which include the generalized second law) forbids this. The result thus constrains the space of allowed wormhole geometries from a different direction than the pointwise NEC.

A subtlety that the literature sometimes handles carelessly: Wall's theorem applies to *achronal* null geodesics under specific assumptions. It does not directly address all null geodesics in all spacetimes, and there are known loopholes involving spacetimes with particular causal structures. The precise implications for wormhole traversability depend on the details of the geometry and on whether the assumptions of the theorem are satisfied. Claiming that Wall's result permits traversable wormholes provided the exotic matter is "sufficiently localized" mischaracterizes the theorem; it is closer to the truth to say that the theorem rules out a large class of would-be traversable configurations and places the burden of proof on proposed exceptions.


## Axisymmetric Spacetime Formalism

Rotating wormholes live in the space of stationary, axially symmetric solutions to the Einstein equations. The mathematical infrastructure for this setting is substantial, and several references in the catalog provide the necessary tools.

### Exact Solutions and Solution-Generating Techniques

Stephani et al. (2003) is the standard compendium of exact solutions to Einstein's equations and the generating techniques used to produce them. For the present purposes, the relevant material includes stationary axisymmetric vacuum solutions (Chapter 19), the Ernst equation and its solution-generating transformations, and rotating matter solutions (Chapter 21). These tools are directly relevant when asking whether a proposed rotating wormhole metric is genuinely a smooth solution of the Einstein(-Maxwell) system or whether it harbors hidden singularities or pathologies.

Dain (2011) reviewed geometric properties and conserved quantities---mass, angular momentum, and the Komar integrals relating them to ADM quantities---in axisymmetric vacuum spacetimes. This material is essential background for any computation involving rotating wormholes, as the definition and measurement of physical quantities like mass and angular momentum require care in spacetimes with nontrivial topology.

### Numerical Relativity in Axisymmetry

Several references provide the computational infrastructure for evolving axisymmetric spacetimes numerically. This is the section of the catalog most directly relevant to computational projects, as the numerical evolution of rotating wormhole initial data requires precisely the tools described here.

Gourgoulhon (2010) offers a comprehensive development of the 3+1 formalism and its application to numerical relativity. The 3+1 decomposition splits the four-dimensional spacetime metric into a spatial three-metric $\gamma_{ij}$, a lapse function $\alpha$, and a shift vector $\beta^i$:

$$ds^2 = -\alpha^2 dt^2 + \gamma_{ij}(dx^i + \beta^i dt)(dx^j + \beta^j dt)$$

The Einstein equations then decompose into constraint equations (Hamiltonian and momentum constraints) that must be satisfied on each spatial slice, and evolution equations for $\gamma_{ij}$ and the extrinsic curvature $K_{ij}$. The choice of gauge (lapse and shift conditions) profoundly affects the stability and accuracy of the numerical evolution. For wormhole spacetimes, gauge choices must respect the nontrivial topology: the throat connects two asymptotic regions, and the coordinate system must handle this smoothly. This is the standard reference for these foundations, and it should be read before attempting any numerical evolution.

Rinne (2013) developed specialized methods for axisymmetric evolutions, including the "cartoon" method (which embeds the axisymmetric problem in a 3D Cartesian grid) and regularization techniques at the symmetry axis. The axis is a coordinate singularity in standard cylindrical or spherical coordinates, and handling it correctly is a nontrivial technical challenge that has derailed many codes.

Choptuik et al. (2003) studied critical phenomena in axisymmetric gravitational collapse. For the scalar field case, the critical solution exhibits discrete self-similarity with an echoing period $\Delta \approx 3.44$. (An earlier analysis, referenced in the companion document, cited $\Delta \approx 0.47$; this is incorrect and appears to conflate the echoing period with a scaling exponent.) The critical collapse work is relevant to wormhole physics primarily as infrastructure: the numerical techniques developed for evolving axisymmetric spacetimes near criticality are directly applicable to evolving wormhole initial data and studying collapse/stability.

Jesse et al. (2020) implemented modern axisymmetric general-relativistic hydrodynamics with adaptive mesh refinement, handling both vacuum and matter regions. This represents the current state of the art for coupling matter sources to axisymmetric spacetimes in numerical relativity.


## Dirac Fields in Curved Spacetime

The EDM wormhole program requires a working theory of spinor fields coupled to gravity---a subject that sits at the intersection of differential geometry, representation theory, and computational physics. The coupling of spinors to curved spacetime is inherently more complex than the scalar or vector field case, because spinors are representations of the local Lorentz group rather than the diffeomorphism group. One must introduce a tetrad (vierbein) field $e^a{}_\mu$ satisfying $g_{\mu\nu} = \eta_{ab} e^a{}_\mu e^b{}_\nu$, and a spin connection $\omega^{ab}{}_\mu$ that mediates parallel transport of spinors. The Dirac equation in curved spacetime then takes the form

$$\left( i \gamma^a e_a{}^\mu D_\mu - m \right) \psi = 0$$

where $D_\mu = \partial_\mu + \frac{1}{4} \omega^{ab}{}_\mu \gamma_a \gamma_b$ is the spinor covariant derivative. The stress-energy tensor derived from the Dirac Lagrangian provides the source for the Einstein equations in the EDM system. The five references in this section provide the essential tools for implementing this coupling numerically.

### The Einstein-Dirac System

Ventrella's 2002 PhD thesis studied massless spin-$\frac{1}{2}$ fields coupled to gravity, developing the tetrad formalism and spinor connection for curved spacetimes and implementing them in a numerical relativity code. Ventrella and Choptuik (2003) used this code to explore critical collapse thresholds for the Einstein-massless-Dirac system, finding that the critical solution has properties distinct from scalar field collapse. This work provides both the mathematical foundations and the numerical infrastructure needed for EDM wormhole evolutions.

### Dirac Equation in Rotating Backgrounds

The separability of the Dirac equation in black hole backgrounds is a classical result that extends, with modifications, to wormhole geometries. Fillion-Gourdeau et al. (2013) developed numerical methods for the time-dependent Dirac equation in axisymmetric geometries, providing computational tools that are applicable whether the background is a black hole or a wormhole.

Kraniotis (2019) derived exact solutions of the massive Dirac equation in Kerr-Newman spacetime, expressing them in terms of confluent Heun functions. These special-function solutions provide analytic benchmarks for numerical codes and illuminate the structure of the spinor mode spectrum. Dariescu et al. (2021) extended this analysis to scattering problems, computing transmission and reflection coefficients for spinor modes---directly relevant to questions about whether fermionic signals can propagate through a wormhole throat.


## Gravitational Lensing and Observational Signatures

The question of whether wormholes can be distinguished from black holes by observation drives a growing body of phenomenological work.

### Ray Tracing and Visualization

Müller (2004) performed early ray-tracing visualizations of Morris-Thorne wormholes, demonstrating the characteristic "double sky" effect: an observer near a wormhole throat sees two copies of the celestial sphere, one from each asymptotic region, distorted by gravitational lensing. The Einstein ring formed by the throat provides a qualitative signature distinct from the photon sphere of a black hole.

James et al. (2015) developed the DNGR (Double Negative Gravitational Renderer) code for the film *Interstellar*, providing both a practical visualization methodology and a physically grounded exploration of wormhole optics. Their key technical contributions include ray-bundle propagation (rather than individual ray tracing) for smooth, high-resolution images, a three-parameter wormhole metric family, and camera-frame geodesic mapping techniques that are applicable beyond the cinematic context.

### Weak-Field Lensing and Distinguishing Signatures

Jusufi and Övgün (2017) calculated deflection angles and magnification for rotating wormholes in the weak-field limit using Gauss-Bonnet methods. Rotation induces asymmetry in the Einstein ring, providing a potential observable distinction from non-rotating configurations.

Rahaman et al. (2021) conducted a comprehensive study of lensing signatures across various wormhole geometries. The distinguishing features from black holes include: absence of photon-sphere caustics (in some geometries), different image multiplicity, and characteristic polarization signatures. However, as the black-bounce interpolation program makes clear, these differences can become arbitrarily small as wormhole parameters approach the black hole limit. The degeneracy between wormholes and near-extremal black holes remains a fundamental challenge for observational discrimination.


## Open Problems and Computational Projects

### Central Theoretical Tensions

Three tensions run through the entire literature surveyed here:

The first is the *energy condition problem*. Traversability in classical GR requires NEC violation. No known classical field provides this (phantom scalars do so by construction, but at the cost of pathological kinetic energy). Quantum effects---Casimir energy, squeezed vacuum states---can violate the NEC, but whether they can do so in the right way, at the right magnitude, and in a stable configuration remains open.

The second is the *stability problem*. Static wormhole solutions are generically unstable under perturbations. Kain's numerical relativity results for EDM wormholes make this explicit, but the problem is older and more general. Even the simplest Ellis-Bronnikov wormholes are unstable under certain perturbation classes. Whether rotation can stabilize wormhole throats---as it stabilizes some configurations in other contexts---is an important open question.

The third is the *junction condition problem*. Symmetric wormhole solutions often require discontinuities in matter fields at the throat. Asymmetric solutions avoid this but introduce other technical challenges, including non-uniqueness and difficulty matching asymptotic conditions on both sides.

### Specific Open Problems

Several concrete problems emerge from the literature:

*Dynamical stability of rotating wormholes.* Kain's work addresses EDM wormholes, but the dynamical stability of Teo-type rotating geometries under generic perturbations has not been studied numerically. This requires axisymmetric numerical relativity evolution of rotating wormhole initial data---a challenging but feasible computational project using existing infrastructure.

*Quantum backreaction beyond semiclassical gravity.* The semiclassical approximation treats the matter quantum mechanically but the geometry classically. For wormhole throats, where curvature can be large and quantum effects are precisely the mechanism invoked to supply exotic matter, the validity of this approximation is questionable. Going beyond it requires either a full theory of quantum gravity or effective field theory techniques that are still under development.

*Observable distinguishing signatures.* The degeneracy between wormholes and black hole mimickers (in shadows, QNMs, and ringdown signals) needs to be quantified precisely, especially for rotating configurations relevant to astrophysical observations. Gravitational-wave echoes---reflections from the throat that would be absent for a true event horizon---remain the most promising qualitative discriminant.

### Computational Project Directions

Several concrete computational projects emerge naturally from this literature:

*Project 1: Rotating wormhole ray tracer.* Implement a geodesic integrator for the Teo metric with user-specified metric functions. Compute shadows, Einstein rings, and image distortions for a grid of parameters. Compare with the Kerr black hole case to quantify the observational degeneracy. The DNGR code (James et al. 2015) provides a methodology; the implementation can use standard ODE integrators (RK4 or adaptive Dormand-Prince) applied to the geodesic equations in the metric above.

*Project 2: Axisymmetric wormhole evolution.* Starting from the Ellis-Bronnikov initial data (or a Teo-type rotating extension), evolve the Einstein-phantom-scalar field equations in axisymmetric 2+1 dimensions using the methods of Rinne (2013) and Jesse et al. (2020). Monitor the apparent horizon finder and track the throat area as a function of time. This provides a direct computational test of dynamical stability.

*Project 3: Black-bounce parameter sweep.* For the Simpson-Visser metric, compute QNMs, greybody factors, and gravitational-wave echo spectra as a function of the interpolation parameter $a/m$. Map the transition from black hole to wormhole in observable space. This project requires only perturbation theory on a fixed background and is accessible with modest computational resources.

*Project 4: EDM wormhole initial data.* Solve the constraint equations for the Einstein-Dirac-Maxwell system on an initial spatial slice, constructing wormhole initial data following Blázquez-Salcedo et al. (2020). This requires solving a coupled system of elliptic PDEs (the Hamiltonian and momentum constraints) with boundary conditions appropriate for asymptotic flatness on both sides of the throat. The numerical methods are standard (multigrid or spectral) but the implementation requires care with the spinor fields at the throat.

### Connections to Other Chapters

The computational techniques surveyed here connect to several other chapters in this project. Numerical relativity methods for axisymmetric evolution draw on the same infrastructure used in binary black hole simulations. The Dirac equation in curved spacetime involves special function theory (Heun functions) that appears in quantum field theory chapters. Gravitational lensing shares ray-tracing methodology with computational optics. And the energy condition constraints connect to the path integral and functional methods treated in the quantum field theory portion of the project.

## Bibliography

### Worm holes

| ID  | Link                                                                                                                                                                                                                              | Notes                                                                                                                     |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| S1  | [Ellis *“Flow through a drain hole”* 1973](https://pubs.aip.org/aip/jmp/article-abstract/14/1/104/223726/Ether-flow-through-a-drainhole-A-particle-model-in?redirectedFrom=fulltext)          | Introduces a traversable “drainhole” geometry as a particle model allowing ether-like flow through a wormhole throat.   |
| S2  | [Visser *“Lorentzian Wormholes”* 1996](https://inspirehep.net/literature/408164)                                                                                                                                                    | Provides a comprehensive treatment of traversable wormhole geometries and their energy-condition violations in GR.       |
| S3  | [Teo *“Rotating traversable wormholes”* 1998](https://arxiv.org/abs/gr-qc/9803098)                                                                                                                                                  | Extends Morris–Thorne wormholes to include rotation and analyzes their metric and embedding properties.                   |
| S4  | [Kashargin and Sushkov *“Slowly rotating scalar field wormholes”* 2008](https://arxiv.org/abs/0809.1923)                                                                                                                           | Develops perturbative solutions for slowly rotating wormholes supported by a scalar field.                                |
| S5  | [Dzhunushaliev et al *“Phantom field wormholes”* 2014](https://arxiv.org/pdf/1409.6978)                                                                                                                                             | Constructs wormhole solutions sustained by phantom scalar fields violating the null energy condition.                    |
| S6  | [Kleihaus and Kunz *“Rotating Ellis Wormholes”* 2014](https://arxiv.org/abs/1409.1503)                                                                                                                                             | Numerically finds and studies rotating generalizations of the Ellis–Bronnikov wormhole.                                  |
| S7  | [Lobo *“Traversable wormholes”* 2016](https://arxiv.org/abs/1604.02082)                                                                                                                                                             | Reviews modern developments in traversable wormhole physics and their astrophysical implications.                        |
| S8  | [Gibbons *“Kerr wormhole”* 2017](https://arxiv.org/abs/1705.07787)                                                                                                                                                                 | Examines wormhole-like extensions of the Kerr solution and their causal structure.                                        |
| S9  | [Kamal et al *“Wormholes with scalar phantom fields”* 2018](https://link.springer.com/article/10.1007/s00601-018-1392-9)                                                                                                            | Analyzes static wormhole configurations supported by minimally coupled phantom scalars.                                  |
| S10 | [Simpson and Visser *“Black-bounce to traversable wormhole”* 2019](https://arxiv.org/abs/1812.07114)                                                                                                                              | Introduces a “black-bounce” metric interpolating between black hole and traversable wormhole geometries.                 |
| S11 | [Huang and Yang *“Charged wormhole and black bounce”* 2019](https://arxiv.org/abs/1909.04603)                                                                                                                                     | Extends black-bounce spacetimes to include electric charge and explores geodesic behavior.                               |
| S12 | [Chew et al *“Rotating wormhole with phantom field”* 2019](https://arxiv.org/abs/1906.08742)                                                                                                                                       | Presents rotating wormhole solutions supported by phantom fields and studies their throat structure.                     |
| S13 | [Blazquez-Salcedo et al *“Einstein Dirac Maxwell Wormholes”* 2020](https://arxiv.org/abs/2010.07317)                                                                                                                               | Discovers wormhole solutions in the coupled Einstein–Dirac–Maxwell system with spinor and electromagnetic fields.         |
| S14 | [Simpson *“Black-bounce to traversable wormhole”* 2021](https://arxiv.org/abs/2110.05657)                                                                                                                                         | Further develops black-bounce models, emphasizing regularity conditions for wormhole throats.                            |
| S15 | [Churilova *“Wormholes without exotic matter”* 2021](https://arxiv.org/abs/2107.05977)                                                                                                                                             | Proposes wormhole geometries that satisfy standard energy conditions by introducing nonminimal field couplings.         |
| S16 | [Emparan et al *“Multi-mouth wormholes”* 2020](https://arxiv.org/abs/2012.07821)                                                                                                                                                        | Introduces solutions describing wormholes with more than two mouths connected through a common throat network.           |
| S17 | [Mazza et al *“Novel rotating wormholes”* 2021](https://arxiv.org/abs/2102.01105)                                                                                                                                                  | Constructs new classes of rotating wormhole metrics and analyzes their stability properties.                             |
| S18 | [Volkov *“Axisymmetric wormholes”* 2021](https://arxiv.org/abs/2109.14496)                                                                                                                                                          | Studies axisymmetric wormhole solutions in various gravity theories and their angular momentum distributions.           |
| S19 | [Konoplya & Zhidenko *“Einstein Maxwell Dirac wormholes”* 2021](https://arxiv.org/abs/2106.05034)                                                                                                                                  | Finds wormhole solutions in the Einstein–Maxwell–Dirac framework including spinor and electromagnetic backreaction.      |
| S20 | [Calhoun et al *“Wormholes in Numerical Relativity”* 2022 ](https://arxiv.org/abs/2210.04905)                                                                                                                                           | Performs numerical simulations of wormhole formation and dynamics in full general relativity.                            |
| S21 | [Kain *“Einstein Maxwell Dirac wormholes in Numerical Relativity”* 2023](https://arxiv.org/abs/2305.11217)                                                                                                                        | Extends numerical relativity studies to the Einstein–Maxwell–Dirac system, showing dynamical wormhole behavior.         |
| S22 | [Kain *“Einstain Maxwell Dirac wormholes in quantum field theory”* 2023](https://arxiv.org/abs/2308.00049)                                                                                                                       | Investigates quantum field theoretic corrections to Einstein–Maxwell–Dirac wormhole backgrounds.                         |
| S23 | [Kain *“Einstein-Dirac system in semiclassical gravity”* 2023](https://arxiv.org/abs/2304.10627)                                                                                                                                  | Explores semiclassical backreaction effects of Dirac fields on wormhole spacetimes.                                      |
| S24 | [Clement & Gal’tsov *“Rotating traversable wormholes in Einstein Maxwell”* 2023](https://arxiv.org/abs/2210.08913)                                                                                                                   | Derives rotating traversable wormholes sourced by electromagnetic fields in Einstein–Maxwell theory.                     |
| S25 | [Kuhfittig *“Wormholes in Einstein’s gravity”* 2023](https://arxiv.org/abs/2312.05266)                                                                                                                                           | Reviews recent exact and numerical wormhole solutions within standard Einstein gravity.                                 |
| S26 | [Kim *“Charged rotating wormholes”* 2024 ](https://arxiv.org/abs/2405.10013)                                                                                                                                                            | Presents charged, rotating wormhole metrics and examines their throat stability.                                         |
| S27 | [Clough et al *“Gravitational waves from warp drive collapse”* 2024](https://arxiv.org/abs/2406.02466)                                                                                                                          | Studies gravitational-wave signatures produced during collapse of warp-drive and wormhole-like spacetimes.               |


---

### Energy Conditions

| ID  | Link                                                                                  | Notes                                                                                                          |
|-----|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| S28 | [Visser *“Arbitrarily small energy violations”* 2003](https://arxiv.org/abs/gr-qc/0301003) | Shows that macroscopic traversable wormholes can be supported by arbitrarily small violations of energy conditions. |
| S29 | [Wall *“Average Null Energy Condition”* 2009](https://arxiv.org/abs/0910.5751)            | Provides proofs of averaged null energy condition theorems in quantum field theory on curved spacetimes.        |

---
### Axisymmetry

| ID  | Link                                                                                                                                                                        | Notes                                                                                                             |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| S30 | [Chandrasekhar & Friedman *“Axisymmetry”* 1972](https://www.osti.gov/biblio/4636844)                                                                                          | Analyzes stability and perturbations of axisymmetric rotating fluid and spacetime configurations.                |
| S31 | [Choptuik et al *“Axisymmetric Collapse”* 2003 ](https://arxiv.org/abs/gr-qc/0301006)                                                                                               | Studies critical phenomena in gravitational collapse under axisymmetry via numerical simulations.                 |
| S32 | [Stephani et al *“Exact Solutions of Einstein’s Equations”* 2003](https://www.cambridge.org/core/books/exact-solutions-of-einsteins-field-equations/11CF6CFCC10CC62B9B299F08C32C37A6#fndtn-information) | Catalogs exact axisymmetric solutions of Einstein’s field equations, including rotating metrics.                 |
| S33 | [Gourgoulhon *“Rotating Relativistic Stars”*  2010](https://arxiv.org/abs/1003.5015)                                                                                           | Describes equilibrium models and oscillations of axisymmetric rotating compact stars in general relativity.      |
| S34 | [Dain *“Axisymmetric Spacetimes”* 2011 ](https://arxiv.org/abs/1106.3106)                                                                                                           | Reviews geometric properties and conserved quantities of axisymmetric vacuum spacetimes.                          |
| S35 | [Rinne *“Axisymmetric Numerical Relativity”* 2013](https://arxiv.org/abs/gr-qc/0601064)                                                                                       | Develops numerical relativity methods specialized for efficient axisymmetric evolutions.                         |
| S36 | [Pashalidis et al *“Rotating Stars in Relativity”* 2017](https://arxiv.org/abs/1612.03050)                                                                                     | Investigates equilibrium and stability of rotating relativistic stars using modern computational techniques.     |
| S37 | [Jesse et al *“Axisymmetric Hydrodynamics in Numerical Relativity”* 2020](https://arxiv.org/abs/2005.01848)                                                                  | Implements axisymmetric general-relativistic hydrodynamics for stellar collapse and merger simulations.           |

---

### Dirac fields in curved spacetime

| ID  | Link                                                                                                                                                                        | Notes                                                                                                               |
|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| S38 | [Ventrella *“Spin 1/2 Fields Coupled to Gravity”* 2002](https://repositories.lib.utexas.edu/items/50cf3613-5141-4f14-9e00-286fb8861896)                                         | Studies coupling of massless spinor fields to gravity and their effect on spacetime dynamics.                       |
| S39 | [Ventrella & Choptuik *“Critical Phenomena in Einstein Massless Dirac”* 2003](https://arxiv.org/abs/gr-qc/0304007)                                                            | Explores critical collapse thresholds and scaling laws for massless Dirac fields in general relativity.             |
| S40 | [Fillion-Gourdeau *“Dirac equation in axisymmetric geometry”* 2013](https://arxiv.org/abs/1303.3781)                                                                        | Solves the Dirac equation in a general axisymmetric curved background and analyzes spinor mode behavior.           |
| S41 | [Kraniotis *“Massive Dirac equation in Kerr-Newman spacetime”* 2019](https://arxiv.org/abs/1801.03157)                                                                       | Derives analytic solutions of the massive Dirac equation in the charged, rotating Kerr–Newman metric.               |
| S42 | [Dariescu et al *“Dirac equation in Kerr-Newman spacetimes”* 2021](https://arxiv.org/abs/2102.03850)                                                                        | Extends analysis of Dirac spinor propagation in Kerr–Newman backgrounds, with applications to scattering problems.  |

---

### Gravitational Lensing

| ID  | Link                                                                                                                                                                                                              | Notes                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| S43 | [Muller *“Visualizing Worhmoles”* 2004](https://pubs.aip.org/aapt/ajp/article-abstract/72/8/1045/529261/Visual-appearance-of-a-Morris-Thorne-wormhole?redirectedFrom=fulltext)                                            | Simulates the optical appearance of a Morris–Thorne wormhole under realistic light-bending conditions.    |
| S44 | [James et al *“Visualizing Interstellar’s Wormhole”* 2015](https://arxiv.org/abs/1502.03809)                                                                                                                          | Produces ray-tracing renderings of the wormhole featured in the film “Interstellar,” illustrating lensing. |
| S45 | [Jusufi & Ovgun *“Lensing a rotating wormhole”* 2017](https://arxiv.org/abs/1708.06725)                                                                                                                             | Calculates deflection angles and image magnification for light passing near a rotating wormhole throat.  |
| S46 | [Rahaman *“Lensing wormholes”* 2021](https://arxiv.org/abs/2108.09930)                                                                                                                                               | Examines lensing signatures of various static and dynamic wormhole geometries and their observational traits. |
