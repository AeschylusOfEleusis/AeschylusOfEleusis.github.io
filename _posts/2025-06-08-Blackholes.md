---
layout:   post
title: "Black holes"
date: 2025-06-08 10:00:00 +0800
categories: [Numerical Relativity]
tags: [Numerical Relativity, Quantum Field Theory, Black holes, Worm holes, Scientific Computing]
math:       true        # enable KaTeX
---
# Notes on Black holes (Draft)

> "The black holes of nature are the most perfect macroscopic objects there are in the universe: the only elements in their construction are our concepts of space and time. And since the general theory of relativity provides only a single unique family of solutions for their descriptions, they are the simplest objects as well."
>
> — S. Chandrasekhar, *The Mathematical Theory of Black Holes* (1983)

## Abstract

Black holes, are considered here with short notes. Sections include a sampling of the literature concerning: 1. The general theory of black holes, 2. Generic behavior of the black hole event horizon, 3. Scattering from black hole sources, and 4. Gravitational radiation from black hole collisions.   

## Introduction

These notes collect and organize the literature on black hole physics as it connects to computation. The subject sits at the intersection of several mathematical traditions: the global geometric methods of Penrose and Hawking, the perturbation theory developed around the Kerr solution by Teukolsky and Chandrasekhar, the membrane paradigm of Thorne and collaborators, and the numerical relativity program that culminated in the 2005 breakthrough simulations of binary black hole coalescence. What unifies these traditions is the event horizon—a null hypersurface whose geometry, dynamics, and response to perturbation encode most of what we mean by "black hole physics."

The notes are organized into four sections reflecting the logical structure of the subject. Section 1 treats the foundational theorems: thermodynamic laws, exact solutions, uniqueness results, and the formation problem. Section 2 addresses the event horizon itself—its geometric characterization, the membrane paradigm, null hypersurface formalism, and the dynamics of horizon mergers. Section 3 covers wave propagation and scattering in black hole backgrounds, from Matzner's pioneering 1968 analysis through modern exact methods. Section 4 treats gravitational radiation: binary dynamics, the self-force problem, data analysis methods, and observational advances.

The bibliography comprises 31 entries (labeled S1–S31) spanning 1968 to 2024. The collection emphasizes mathematical rigor and geometric insight, reflecting the character of black hole physics as one of the most precisely formulated areas of theoretical physics. Several entries serve double duty—Wald's *General Relativity* (S3), for instance, provides both the causal-structure machinery needed for precise horizon definitions and the variational framework underlying the first law of black hole mechanics.

A note on scope: these notes focus on classical and semiclassical black hole physics as it bears on computation. Quantum gravity proper—the information paradox, firewall debates, holographic entanglement—lies outside the present scope, though the thermodynamic foundations treated in Section 1 connect directly to those questions. The emphasis throughout is on the mathematical structures that underlie numerical implementation: the 3+1 decomposition, null surface geometry, perturbation theory, and geodesic focusing.

The intellectual lineage of these notes deserves brief comment. The scattering theory of Section 3 traces to Matzner's 1968 analysis, which predates the golden age of black hole thermodynamics (1971–1974) and even the Penrose process (1969). The perturbation theory underlying gravitational wave template construction was developed by Regge and Wheeler (1957), Zerilli (1970), and Teukolsky (1973), decades before the first detection. The membrane paradigm of Section 2 emerged from astrophysical motivations in the 1980s. The numerical relativity breakthrough came in 2005. And the observational era began on September 14, 2015, with the detection of GW150914. The bibliography thus spans five decades of theoretical development that, taken together, constitutes one of the most complete correspondences between mathematical prediction and experimental confirmation in the history of physics.

The organization into four sections reflects a logical rather than historical ordering. One reads the general theorems first because they define the objects of study; the event horizon section second because the horizon is the defining feature of a black hole; scattering theory third because it provides the link between geometry and observable quantities; and gravitational wave physics last because it is the observational payoff. Within each section, the sources are arranged to support a progressive development of understanding, from foundational to specialized.


## 1. General Theorems

The mathematical theory of black holes rests on a small number of foundational results: the laws of black hole mechanics, the uniqueness theorems for stationary solutions, the singularity theorems, and the formation problem. These results establish what black holes are (the exact solutions), what they must do (the thermodynamic laws), and when they form (trapped surface criteria). The literature in this section provides the conceptual and mathematical infrastructure on which everything else depends.

### 1.1 Thermodynamic Foundations

The analogy between black hole mechanics and thermodynamics, established in its definitive form by Bardeen, Carter, and Hawking (1973) [S1], remains one of the most remarkable structural correspondences in theoretical physics. The four laws are:

- **Zeroth law.** The surface gravity $\kappa$ of a stationary black hole is constant over the event horizon. This is the analog of thermodynamic equilibrium: just as temperature is uniform throughout a body in thermal equilibrium, surface gravity is uniform across the horizon of a stationary black hole.

- **First law.** For perturbations of a Kerr–Newman black hole, the changes in mass $M$, horizon area $A$, angular momentum $J$, and charge $Q$ satisfy
$$dM = \frac{\kappa}{8\pi}\,dA + \Omega\,dJ + \Phi\,dQ,$$
where $\Omega$ is the angular velocity and $\Phi$ the electrostatic potential at the horizon. The identification $\kappa/8\pi \leftrightarrow T$ and $A \leftrightarrow S$ gives the Bekenstein–Hawking entropy formula $S = A/4$ (in natural units).

- **Second law.** The area of the event horizon never decreases in any classical process: $\delta A \geq 0$. Hawking's area theorem, proved using the Raychaudhuri equation and the null energy condition, is the gravitational analog of the second law of thermodynamics.

- **Third law.** It is impossible to reduce the surface gravity to zero by any finite sequence of operations—the analog of the unattainability formulation of the third law.

The Hawking (1973) paper [S1] treated these laws as a formal analogy. Bekenstein had already suggested that the analogy was more than formal—that black holes carry genuine entropy proportional to their area. Hawking's 1974 discovery that quantum effects cause black holes to radiate thermally at temperature $T = \kappa/2\pi$ confirmed Bekenstein's conjecture and elevated the laws of black hole mechanics to laws of black hole thermodynamics. The present notes do not cover Hawking radiation in detail, but the thermodynamic laws inform several computational diagnostics: monitoring horizon area growth in numerical simulations provides a check on the second law, while the first law relates the mass and spin extracted from gravitational waveforms to horizon geometry.

The biographical overview by Carr et al. (2020) [S9] provides historical context for Hawking's contributions, including the area theorem, the singularity theorems (with Penrose), and the information paradox. As a survey of one person's trajectory through the field, it serves as a useful map of how these foundational results developed and interconnected.

### 1.2 Mathematical Framework

Three texts provide the mathematical infrastructure. They occupy different positions in the difficulty landscape and serve complementary purposes.

**Wald (1984)** [S3] is the standard graduate-level treatment of general relativity, distinguished from other texts (Misner–Thorne–Wheeler, Carroll, Schutz) by its emphasis on global methods. The later chapters develop Penrose diagrams, causal structure, the Penrose and Hawking singularity theorems, and the uniqueness theorems for stationary black holes. For readers approaching black hole physics through numerical relativity, Wald's treatment of the initial value formulation (Chapter 10) and his careful definitions of event horizons, apparent horizons, and trapped surfaces (Chapter 12) are essential. The mathematical precision of the definitions matters computationally: the event horizon is a global construct requiring knowledge of the entire future development of the spacetime, while the apparent horizon is quasi-local and can be found on individual time slices—a distinction with direct algorithmic consequences.

**Chandrasekhar (1983)** [S2] is a different sort of text entirely. Where Wald develops the general framework, Chandrasekhar performs exhaustive calculations for the specific exact solutions. The book treats the Schwarzschild, Reissner–Nordström, Kerr, and Kerr–Newman solutions in turn, developing perturbation theory for each and analyzing their stability properties and quasi-normal mode spectra. The level of calculational detail is extreme by modern standards; Chandrasekhar works through every separation of variables and every radial equation explicitly. For the reader willing to follow the calculations, the reward is complete mastery of the perturbation theory that underlies gravitational wave template construction. The quasi-normal mode spectra computed here are the theoretical predictions tested by LIGO/Virgo ringdown analyses.

**Chruściel (2020)** [S8] represents the modern mathematical approach. Beginning with global Lorentzian geometry (causal structure, topology, geodesic completeness), the text develops the theory of trapped surfaces, apparent horizons, and uniqueness theorems with full mathematical rigor. The treatment of "numerical black holes"—relating the mathematical definitions to objects that can be located on computational grids—is particularly relevant for the computational focus of these notes. This text occupies the highest position in the difficulty hierarchy: it assumes familiarity with differential geometry at the level of a mathematics (not physics) graduate program.

### 1.3 Formation of Black Holes

**Christodoulou (2008)** [S4] addresses a question that had remained open since the singularity theorems of the 1960s: can black holes form dynamically from regular initial data, without symmetry assumptions? The Penrose and Hawking theorems established that singularities form under generic conditions, but singularity formation and black hole formation are logically distinct—a singularity could in principle be naked (visible to distant observers) rather than hidden behind a horizon.

Christodoulou's monograph proves that trapped surfaces—and hence black holes, given cosmic censorship—can form from the focusing of gravitational waves in vacuum spacetimes. The proof introduces the "short pulse method," constructing initial data as a thin shell of gravitational radiation and showing that the nonlinear focusing of this pulse generates a trapped surface. The result establishes that Minkowski spacetime, while stable against small perturbations (the Christodoulou–Klainerman theorem), is dynamically unstable to black hole formation under sufficiently strong gravitational wave focusing.

The mathematical machinery is formidable: the proof uses the full Einstein equations in double null coordinates, derives sharp estimates on the Riemann curvature tensor, and tracks the evolution of null geodesic congruences through the focusing region. For the computationally minded reader, the relevant insight is structural: the formation mechanism is nonlinear focusing of null geodesics, governed by the Raychaudhuri equation (treated in Section 2.3 below). The short pulse method has since been extended and simplified by Klainerman, Luk, and Rodnianski, among others.

### 1.4 The Kerr Solution

Astrophysical black holes rotate. The Kerr solution (1963), describing the unique stationary, axisymmetric, vacuum black hole, is therefore the physically relevant exact solution. Three entries provide complementary perspectives.

**Kerr (2008)** [S5] is a historical and technical account by Roy Kerr of his discovery of the rotating black hole metric. The paper describes the algebraic approach that led to the solution—the use of Kerr–Schild coordinates, null tetrads, and algebraic classification of the Weyl tensor—and situates the discovery in the context of 1960s general relativity. Kerr–Schild coordinates have found renewed importance in numerical relativity: they provide horizon-penetrating coordinates that avoid the coordinate singularity of Boyer–Lindquist coordinates at the event horizon, making them natural for computational work.

**Wiltshire, Visser, and Scott (2009)** [S6] edit a comprehensive monograph on Kerr spacetime geometry, treating geodesic structure, the Penrose process (energy extraction from the ergosphere), frame dragging, and the multiple horizons (inner and outer) of the Kerr solution. The edited volume format provides multiple perspectives on the same geometric object, which is useful given the richness of Kerr phenomenology.

**Teukolsky (2014)** [S7] reviews the perturbation theory of the Kerr metric, centered on the Teukolsky master equation. The remarkable mathematical fact underlying this work is the separability of the wave equation in Kerr spacetime—a property that Chandrasekhar called "miraculous" and that depends on the existence of a hidden symmetry encoded in the Killing tensor. The Teukolsky equation governs perturbations of all spin weights (scalar, electromagnetic, gravitational) in a single formalism. Its solutions yield quasi-normal mode frequencies (the characteristic "ringing" of a perturbed black hole), scattering amplitudes, and stability results. For gravitational wave physics, the Teukolsky formalism provides the theoretical backbone for ringdown waveform templates and black hole spectroscopy.

The separability deserves further comment because it is both mathematically deep and computationally consequential. The Kerr metric admits four constants of motion for geodesics: energy $E$, axial angular momentum $L_z$, rest mass $\mu$, and the Carter constant $Q$—the last being associated with the Killing tensor rather than a Killing vector, and hence a "hidden" symmetry with no simple spacetime interpretation. This four-constant integrability makes the geodesic equations fully separable, reducing the problem to quadratures. For wave equations, the analogous property is that the angular and radial dependences separate completely, reducing partial differential equations to ordinary differential equations (ODEs). This reduction from PDEs to ODEs is what makes analytic progress possible: QNM frequencies can be computed to high precision, scattering cross-sections can be evaluated by numerical integration of ODEs, and the stability of the Kerr solution can be analyzed mode by mode. Without separability, one would be forced to solve the full PDE system numerically—a vastly harder computational problem.

The perturbative stability of the Kerr solution remains, after fifty years, an open mathematical problem. Whiting (1989) proved mode stability (no exponentially growing modes), and recent work by Dafermos, Holzegel, Rodnianski, and others has established quantitative decay estimates for scalar fields on Kerr backgrounds. The full nonlinear stability of Kerr, analogous to the Christodoulou–Klainerman stability proof for Minkowski space, remains unproven—though significant progress has been made by Klainerman and Szeftel.


## 2. The Event Horizon

The event horizon is the central geometric object in black hole physics. Defined globally as the boundary of the causal past of future null infinity, it is a null hypersurface whose generators are null geodesics that, once they join the horizon, never leave. The geometry of this surface—its expansion, shear, and topology—encodes the dynamical state of the black hole. Computing the event horizon in numerical simulations requires tracking null geodesics backward in time from late in the evolution, a fundamentally global construction that distinguishes it from the quasi-local apparent horizon (the outermost marginally trapped surface on a given time slice).

### 2.1 The Membrane Paradigm

**Thorne, Price, and Macdonald (1986)** [S10–S11] introduced the membrane paradigm, a reformulation of black hole physics that treats the event horizon as a two-dimensional membrane endowed with physical properties. The horizon membrane has:

- An electrical surface resistivity of $377\,\Omega$ (the impedance of free space—a coincidence that reflects the universality of the coupling between electromagnetic fields and the horizon).
- A shear viscosity and bulk viscosity, governing the dissipative response of the horizon to tidal perturbations.
- A surface temperature proportional to the surface gravity (the Hawking temperature).

The power of the paradigm is computational: it replaces the global causal structure of the black hole spacetime with boundary conditions on a two-dimensional surface. Electromagnetic fields threading the horizon satisfy equations formally identical to those of a resistive membrane in flat spacetime. Tidal deformations of the horizon are governed by a viscous fluid equation. This reformulation provides physical intuition for phenomena—the Blandford–Znajek mechanism for jet production, tidal heating of the horizon during inspiral—that are difficult to visualize in the full four-dimensional geometry.

For numerical relativity, the membrane paradigm motivates the use of horizon quantities (area, angular momentum, multipole moments) as simulation diagnostics. The horizon's viscous response also connects to modern developments in the fluid/gravity correspondence, where the long-wavelength dynamics of certain black branes is exactly dual to Navier–Stokes hydrodynamics.

### 2.2 Null Hypersurface Geometry

The mathematical characterization of the event horizon as a null hypersurface requires machinery beyond the standard 3+1 decomposition of spacelike surfaces. Two references develop this formalism.

**Poisson (2004)** [S12] provides a modern toolkit for relativists, with detailed treatments of the geometry of null surfaces, junction conditions (Israel formalism), and the boundary conditions appropriate for horizons in numerical simulations. The text is pitched at the working relativist rather than the mathematician, making it more immediately applicable to computational work than the more rigorous treatments of Chruściel.

**Gourgoulhon and Jaramillo (2005)** [S13] develop a 3+1 perspective on null hypersurface geometry, connecting the isolated horizon formalism of Ashtekar and collaborators with the numerical relativity 3+1 decomposition. This paper bridges two communities: the mathematical relativists who developed quasi-local horizon definitions (isolated horizons, dynamical horizons, trapping horizons) and the numerical relativists who need to locate and characterize horizons on computational grids. The 3+1 reformulation of Damour's black hole mechanics provides a unified framework for extracting physical quantities (mass, angular momentum, multipole moments) from numerically computed horizons.

The distinction between quasi-local and global horizon definitions is computationally significant. The event horizon requires knowledge of the full future evolution (one must determine which null geodesics eventually escape to infinity), while the apparent horizon—the outermost marginally trapped surface—can be found on a single time slice by solving an elliptic equation. In practice, numerical simulations locate apparent horizons during the evolution (using, e.g., the methods of Thornburg) and construct the event horizon in post-processing by integrating null geodesics backward from late times.

The hierarchy of horizon definitions merits explicit enumeration, as the terminology is a source of persistent confusion. An **event horizon** is the boundary of the causal past of future null infinity—a teleological definition requiring knowledge of the entire future spacetime. An **apparent horizon** is the outermost marginally trapped surface on a given spacelike slice, defined locally in time but depending on the choice of foliation. An **isolated horizon** (Ashtekar et al.) is a null surface satisfying quasi-equilibrium conditions (vanishing expansion, time-independent induced geometry), appropriate for black holes that are not actively accreting or merging. A **dynamical horizon** (Ashtekar and Krishnan) generalizes the isolated horizon to non-equilibrium situations, defined as a spacelike surface foliated by marginally trapped 2-spheres.

For numerical work, the apparent horizon is the primary real-time diagnostic because it can be found algorithmically on each time slice. The standard method solves the equation $\theta_{(\ell)} = 0$ for the outgoing null expansion on trial surfaces, typically using spectral methods (expanding the surface in spherical harmonics) with Newton's method iteration. The event horizon, computed in post-processing, provides the true boundary and the correct area for thermodynamic considerations, but at the cost of requiring the full spacetime history.

### 2.3 The Raychaudhuri Equation

**Kar and SenGupta (2007)** [S14] provide a comprehensive review of the Raychaudhuri equation, the fundamental evolution equation for geodesic congruences in curved spacetime. For a congruence of null geodesics with tangent vector $k^a$, the Raychaudhuri equation governs the evolution of the expansion $\theta$:

$$\frac{d\theta}{d\lambda} = -\frac{1}{2}\theta^2 - \sigma_{ab}\sigma^{ab} + \omega_{ab}\omega^{ab} - R_{ab}k^a k^b,$$

where $\sigma_{ab}$ is the shear, $\omega_{ab}$ is the twist, and $R_{ab}$ is the Ricci tensor. For a hypersurface-orthogonal congruence (vanishing twist), the null energy condition ($R_{ab}k^a k^b \geq 0$) ensures that $\theta$ decreases monotonically, driving geodesics to focus and form caustics.

This equation is the workhorse of classical black hole physics. Hawking's area theorem follows from it: the generators of the event horizon form a twist-free null congruence, so the null energy condition guarantees non-decreasing expansion, which in turn guarantees non-decreasing area. The singularity theorems of Penrose and Hawking use the Raychaudhuri equation to show that geodesic focusing leads to geodesic incompleteness. Christodoulou's formation proof (Section 1.3) is ultimately an analysis of when the nonlinear terms in the Raychaudhuri equation dominate.

Computationally, the Raychaudhuri equation governs the behavior of null geodesic generators that constitute the event horizon. When generators join the horizon (at caustics or "crease" points), the expansion undergoes characteristic behavior that must be tracked accurately in numerical event-horizon finders.

### 2.4 Merger Dynamics

The geometry of the event horizon during a binary black hole merger is topologically nontrivial. Before merger, there are two disjoint horizons; after merger, there is one. The transition involves a topology change on the horizon surface, occurring through the formation and annihilation of "crease sets"—singularities in the null generators where new generators join the horizon.

**Emparan and Martínez (2016)** [S15] study event horizon dynamics during mergers, particularly in higher-dimensional spacetimes where the richer topology of horizon cross-sections allows novel phenomena (e.g., "pinch-off" transitions from a single connected horizon to multiple components, the reverse of merger). While the higher-dimensional aspects go beyond the scope of astrophysical computation, the analysis of topology change mechanisms applies equally to the four-dimensional case.

**Emparan et al. (2018)** [S16] investigate the extreme mass ratio limit, where a small black hole spirals into a much larger one. In this limit the deformation of the large horizon can be treated perturbatively, but the merger itself remains a genuinely nonlinear event. The extreme mass ratio regime is the target of the LISA space-based gravitational wave detector, making horizon dynamics in this regime both mathematically tractable and observationally relevant.

**Gadioux (2024)** [S17] examines the formation and evolution of crease sets—the loci where new null generators join the event horizon through caustic singularities. These geometric features encode information about the merger history and provide a diagnostic for the dynamical state of the horizon. This recent work connects to the broader program of understanding event horizon topology change, building on earlier work by Siino, Husa and Winicour, and others on the structure of the event horizon during gravitational collapse and merger.


## 3. Scattering from Black Holes

The scattering of waves from black holes connects the geometric theory of Sections 1–2 to observable quantities: absorption cross-sections, scattering amplitudes, quasi-normal mode frequencies, and (ultimately) gravitational waveforms. The mathematical framework is the theory of wave equations on curved backgrounds—the Klein–Gordon, Maxwell, and linearized Einstein equations in Schwarzschild and Kerr spacetimes. The remarkable separability properties of these equations in the Kerr background (encoded in the Teukolsky equation) make analytic progress possible, while the physical phenomena—glory scattering, superradiance, quasi-normal ringing—provide both intuition and computational benchmarks.

### 3.1 Foundations

**Matzner (1968)** [S18] established the scattering cross-section for massless scalar waves by a Schwarzschild black hole, pioneering the analysis of wave-optical phenomena in black hole spacetimes. The key physical insight is that the photon sphere at $r = 3M$ acts as a critical impact parameter: waves with angular momentum near the critical value orbit multiple times before scattering, producing interference effects analogous to glory scattering in optics. The forward scattering amplitude diverges logarithmically (the gravitational analog of Coulomb scattering), and the backward glory produces a characteristic diffraction pattern whose angular scale is set by the photon sphere radius.

This early work is foundational for several reasons. First, it established the partial wave decomposition as the primary computational tool for black hole scattering, expanding the scattered field in spin-weighted spherical harmonics and solving ordinary differential equations for the radial functions. Second, it identified the physically important length scales: the Schwarzschild radius $2M$, the photon sphere $3M$, and the wavelength $\lambda$ of the incident radiation. The dimensionless ratio $M/\lambda$ governs the relative importance of geometric optics ($M/\lambda \gg 1$) versus wave-optical ($M/\lambda \sim 1$) effects. Third, it motivated the development of more sophisticated approaches—WKB methods, complex angular momentum techniques, exact analytic solutions—that the subsequent literature pursues.

### 3.2 Spectral Theory

**Persides (1973)** [S19–S20] investigated the spectral properties of the Laplace operator in Schwarzschild spacetime and derived the radial wave equation governing scattering. These two papers establish the mathematical framework—the function spaces, boundary conditions, and spectral properties—for the scattering problem as a well-posed mathematical question. The radial equation, after separation of angular variables, takes the form of a one-dimensional Schrödinger equation with an effective potential that depends on the black hole mass, the angular momentum quantum number $\ell$, and the spin of the field. The effective potential has a single maximum near the photon sphere and vanishes at both the horizon ($r \to 2M$) and spatial infinity ($r \to \infty$), giving a standard scattering problem with well-defined transmission and reflection coefficients.

The spectral theory perspective is important for understanding quasi-normal modes (QNMs)—the damped oscillations of a perturbed black hole. QNMs are not normal modes in the usual sense (the operator is not self-adjoint due to radiation boundary conditions at the horizon and infinity), but rather resonances—poles of the scattering matrix in the complex frequency plane. The machinery Persides develops is the starting point for the QNM calculations that are central to gravitational wave ringdown analysis.

### 3.3 Comprehensive Treatments

**Futterman, Handler, and Matzner (1988)** [S21] is the comprehensive monograph on scattering from black holes, covering scalar, electromagnetic, and gravitational waves in Schwarzschild and Kerr backgrounds. The text develops the partial wave formalism systematically, treats absorption cross-sections (how much energy a black hole captures), glory scattering (the backward-directed interference pattern), and superradiant amplification (the wave analog of the Penrose process, where waves scattered from a rotating black hole can extract rotational energy). This book is the primary reference for anyone implementing scattering calculations.

**Bezerra et al. (2013)** [S22] extend the scattering formalism to charged (Reissner–Nordström) and rotating (Kerr) backgrounds. The separation of the Klein–Gordon equation in Kerr–Newman spacetime introduces the angular eigenvalue problem (spheroidal harmonics) as an additional computational element.

**Li et al. (2022)** [S23] present exact analytic solutions for certain black hole scattering problems, advancing beyond the perturbative and numerical treatments of earlier work. Exact solutions provide benchmarks for numerical codes and can reveal qualitative features—such as the analytic structure of the scattering amplitude in the complex angular momentum plane—that approximate methods obscure.


## 4. Gravitational Waves

The detection of gravitational waves from binary black hole mergers by LIGO in 2015 transformed black hole physics from a theoretical discipline into an observational science. The theoretical infrastructure underlying gravitational wave astronomy includes post-Newtonian approximations for the inspiral phase, numerical relativity for the merger, and perturbation theory for the ringdown. The self-force program provides a systematic framework for extreme mass ratio systems. The entries in this section cover the theoretical, computational, and observational aspects of gravitational radiation from black hole systems.

### 4.1 Binary Dynamics

**Trimble and Thorne (2018)** [S24] review the physics of binary systems and their gravitational wave signatures. The conceptual framework for understanding gravitational waves from binaries involves three regimes, each requiring different analytical and computational tools:

The **inspiral** phase, where the binary components orbit at separations much larger than the Schwarzschild radii, is well described by post-Newtonian (PN) theory—a systematic expansion in powers of $v/c$ beyond Newtonian gravity. The leading gravitational wave emission is quadrupolar, with the Einstein quadrupole formula giving the luminosity $L = (32/5)(M\omega)^{10/3}$ for a circular binary with total mass $M$ and orbital frequency $\omega$ (in geometric units).

The **merger** phase, where the two bodies plunge together and their horizons coalesce, can only be computed by solving the full Einstein equations numerically. This phase produces the peak gravitational wave amplitude and encodes information about the nonlinear dynamics of general relativity that is inaccessible to perturbative methods. The 2005 breakthrough by Pretorius, using generalized harmonic coordinates, and the independent 2006 successes by Campanelli et al. (moving punctures with BSSN formalism) and Baker et al. (similar approach), demonstrated that the merger phase is computationally tractable and produces waveforms in remarkable agreement with the post-Newtonian and perturbation theory predictions in the appropriate limits. The merger waveform is dominated by the $(\ell,m) = (2,2)$ mode and lasts only a few cycles, but it carries the most luminous gravitational wave emission—during the peak, GW150914 radiated energy at a rate exceeding the combined luminosity of all stars in the observable universe.

The **ringdown** phase, where the newly formed black hole settles to a Kerr solution by radiating quasi-normal modes, is described by black hole perturbation theory. The QNM frequencies depend only on the mass and spin of the final black hole (by the no-hair theorem), making ringdown observations a test of general relativity. The dominant mode is the fundamental $(\ell,m) = (2,2)$ mode, with frequency $f_{220} \approx 1.525\,(100\,M_\odot/M)\,\text{kHz}$ and damping time $\tau_{220} \approx 0.856\,(M/100\,M_\odot)\,\text{ms}$ for a Kerr black hole with spin $a/M = 0.67$. Detecting multiple QNM overtones would enable black hole spectroscopy—a direct test of the no-hair theorem and a probe of the strong-field regime of general relativity.

### 4.2 Self-Force and Radiation Reaction

The self-force program addresses the problem of motion and radiation reaction for a compact object orbiting a much larger black hole—the extreme mass ratio inspiral (EMRI) scenario. The physical question is: how does the gravitational field of a small body affect its own trajectory? The answer involves regularizing the divergent self-field of a point particle in curved spacetime and extracting the finite "radiation reaction" force that drives the inspiral.

**Quinn (2000)** [S25] analyzes the self-force for a scalar charge in curved spacetime, which serves as a technically simpler model problem for the gravitational case. The scalar self-force problem shares the essential mathematical structure—a Green's function that must be decomposed into a singular "direct" part (to be subtracted) and a regular "tail" part (which contributes to the self-force)—without the gauge complications of the gravitational case.

**de Felice and Bini (2010)** [S26] develop the formalism for classical measurements in curved spacetimes, addressing how local observers characterize tidal fields, precession effects, and radiative forces. This work provides the conceptual framework for interpreting self-force results in terms of physically measurable quantities.

**Poisson, Pound, and Vega (2011)** [S27] is the comprehensive Living Reviews article on the motion of point particles in curved spacetime. The article develops the gravitational self-force through matched asymptotic expansions—treating the small body's neighborhood with its own strong-field solution and matching to the external spacetime treated as a perturbation of the large black hole's geometry. The resulting "MiSaTaQuWa" equation (named for Mino, Sasaki, Tanaka, Quinn, and Wald) gives the regularized equation of motion. This formalism underlies the waveform models being developed for LISA, the space-based gravitational wave detector that will observe EMRIs in the millihertz band.

The self-force problem illustrates a recurring theme in these notes: the interplay between exact mathematical structure and computational implementation. The formal solution involves the retarded Green's function of the linearized Einstein equation, which can be decomposed into a "direct" part (supported on the past light cone) and a "tail" part (supported inside the light cone, arising from backscattering off the spacetime curvature). The direct part diverges at the particle's location and must be regularized; the tail part is finite and provides the physical self-force. Several regularization schemes have been developed—mode-sum regularization (Barack and Ori), effective source methods (Vega and Detweiler), and puncture schemes—each with distinct computational trade-offs. The first-order self-force is now computed routinely for generic orbits in Kerr spacetime, and second-order calculations (needed for LISA accuracy requirements) are an active area of development.

The gravitational self-force connects to the broader theme of radiation reaction in field theories. The electromagnetic analog—the Abraham–Lorentz–Dirac equation for the self-force on a charged particle—has been known since the early twentieth century and exhibits pathologies (runaway solutions, preacceleration) that the gravitational case largely avoids due to the equivalence principle. The scalar model problem treated by Quinn [S25] shares the mathematical structure of the gravitational case without the gauge complications, making it a valuable testing ground for regularization methods and numerical algorithms.

### 4.3 Detection and Data Analysis

**Jaranowski and Królak (2023)** [S28] survey the statistical and computational methods for analyzing gravitational wave signals in detector data. The dominant technique is matched filtering: cross-correlating the detector output with a bank of theoretical waveform templates and searching for statistically significant matches. The method requires accurate waveform models spanning the parameter space (masses, spins, sky location, orientation), which in turn requires the inspiral-merger-ringdown waveform models produced by combining post-Newtonian theory, numerical relativity, and perturbation theory. The review covers the Gaussian noise case in detail, treating signal detection as a hypothesis testing problem within the Neyman–Pearson framework, and discusses parameter estimation using Bayesian methods.

**Romano and Cornish (2017)** [S29] review a complementary detection problem: the stochastic gravitational wave background—the superposition of unresolved signals from many sources. The stochastic background has multiple astrophysical components (unresolved compact binaries, supernovae, neutron star mergers) and potentially cosmological components (inflation, phase transitions, cosmic strings). Detection requires cross-correlating the outputs of multiple detectors, exploiting the fact that the gravitational wave signal is correlated between detectors while the noise is not. The overlap reduction function, which encodes the detector geometry and the antenna pattern, determines the sensitivity of a given detector pair to the stochastic background.

### 4.4 Observational Breakthroughs

**LIGO Scientific Collaboration et al. (2016)** [S30] announced the first direct detection of gravitational waves: the event GW150914, observed on September 14, 2015. The signal matched the waveform predicted by general relativity for the inspiral, merger, and ringdown of two black holes with masses approximately $36\,M_\odot$ and $29\,M_\odot$ at a luminosity distance of roughly 410 Mpc. The final black hole had mass approximately $62\,M_\odot$ with spin parameter $a/M \approx 0.67$, meaning roughly $3\,M_\odot c^2$ of energy was radiated as gravitational waves in less than a second.

The detection confirmed several theoretical predictions simultaneously: the existence of gravitational waves (predicted by Einstein in 1916), the existence of stellar-mass binary black holes (whose formation channels had been debated), and the accuracy of numerical relativity waveform predictions for the merger phase. Subsequent observing runs have detected dozens of binary black hole mergers, enabling population studies and increasingly precise tests of general relativity.

The significance of GW150914 for the program of these notes cannot be overstated. The matched filter analysis that identified the signal required a bank of waveform templates produced by combining post-Newtonian theory (inspiral), numerical relativity (merger), and black hole perturbation theory (ringdown)—precisely the three theoretical frameworks treated in Sections 1, 3, and 4 of these notes. The parameter estimation that determined the source masses and spin used Bayesian methods with the same template families. And the test of general relativity—comparing the observed ringdown frequency with the prediction from the no-hair theorem—relied on the QNM calculations rooted in the Teukolsky formalism of Section 1.4 and the scattering theory of Section 3.

The gravitational wave catalog has grown rapidly since GW150914. The first three observing runs (O1, O2, O3) of LIGO and Virgo detected approximately 90 compact binary coalescences, predominantly binary black hole mergers but also binary neutron star mergers (GW170817, with its electromagnetic counterpart) and neutron star–black hole mergers. The fourth observing run (O4), begun in 2023, has further expanded the catalog. The population of observed binary black holes has yielded constraints on formation channels (isolated binary evolution versus dynamical formation in dense stellar environments), the black hole mass spectrum (including evidence for features at masses where pair-instability supernovae are expected to suppress black hole formation), and the distribution of black hole spins.

*Bibliographic note.* The original source page links this entry to arXiv:1304.0670, which is the Advanced LIGO sensitivity and observing scenarios paper rather than the detection announcement. The detection paper is Abbott et al. (2016), "Observation of Gravitational Waves from a Binary Black Hole Merger," *Physical Review Letters* 116, 061102 (arXiv:1602.03837).

**Pretorius (2023)** [S31] provides a comprehensive survey of gravitational wave physics by one of the pioneers of numerical relativity. Pretorius achieved the first stable simulation of a binary black hole merger and gravitational wave emission in 2005—a breakthrough that, together with the independent work of Campanelli et al. and Baker et al. in 2006, solved a problem that had resisted numerical attack for decades. The review covers the current state of gravitational wave observations, theoretical developments, and prospects for next-generation detectors (Einstein Telescope, Cosmic Explorer, LISA).


## 5. Bibliographic Assessment

### 5.1 Reference Summary

The following table summarizes all 31 entries organized by section, with year and topic.

| ID | Author(s) | Year | Topic |
|:---|:----------|:-----|:------|
| S1 | Bardeen, Carter, Hawking | 1973 | Four laws of black hole mechanics |
| S2 | Chandrasekhar | 1983 | Mathematical theory of black holes |
| S3 | Wald | 1984 | General relativity (graduate text) |
| S4 | Christodoulou | 2008 | Formation of black holes (rigorous proof) |
| S5 | Kerr | 2008 | Kerr solution: discovery and context |
| S6 | Wiltshire, Visser, Scott (eds.) | 2009 | The Kerr spacetime (edited volume) |
| S7 | Teukolsky | 2014 | Kerr perturbation theory and separability |
| S8 | Chruściel | 2020 | Geometry of black holes (rigorous) |
| S9 | Carr et al. | 2020 | Hawking: biographical and scientific overview |
| S10–11 | Thorne, Price, Macdonald | 1986 | Membrane paradigm |
| S12 | Poisson | 2004 | Relativist's toolkit: null surface geometry |
| S13 | Gourgoulhon, Jaramillo | 2005 | 3+1 formalism for null hypersurfaces |
| S14 | Kar, SenGupta | 2007 | Raychaudhuri equation (review) |
| S15 | Emparan, Martínez | 2016 | Event horizon fusion dynamics |
| S16 | Emparan et al. | 2018 | Extreme mass ratio horizon dynamics |
| S17 | Gadioux | 2024 | Crease set evolution on event horizons |
| S18 | Matzner | 1968 | Scalar wave scattering (Schwarzschild) |
| S19–20 | Persides | 1973 | Spectral theory and radial wave equation |
| S21 | Futterman, Handler, Matzner | 1988 | Scattering from black holes (monograph) |
| S22 | Bezerra et al. | 2013 | Scattering: charged and rotating holes |
| S23 | Li et al. | 2022 | Exact scattering solutions |
| S24 | Trimble, Thorne | 2018 | Binary systems and gravitational radiation |
| S25 | Quinn | 2000 | Scalar self-force and radiation reaction |
| S26 | de Felice, Bini | 2010 | Classical measurements in curved spacetime |
| S27 | Poisson, Pound, Vega | 2011 | Gravitational self-force (Living Reviews) |
| S28 | Jaranowski, Królak | 2023 | Gravitational wave data analysis |
| S29 | Romano, Cornish | 2017 | Stochastic gravitational wave backgrounds |
| S30 | LIGO/Virgo Collaboration | 2016 | First gravitational wave detection |
| S31 | Pretorius | 2023 | Survey of gravitational wave physics |

### 5.2 Link Verification

An independent link audit of the source page identified several categories of access issues:

**Publisher-gated links (HTTP 403 or JavaScript barriers).** S1 (World Scientific), S2 (Oxford University Press), S6 (Cambridge University Press), S10 (Science), S15 (World Scientific), S18 (AIP), S20 (AIP). For these, arXiv preprints are available for S7, S9, S13, S14, and others, but several foundational texts (S2, S3, S6) are available only through institutional access. A general recommendation: prefer stable DOI landing pages or arXiv links over publisher-specific URLs that may break under paywall changes.

**ArXiv links verified and accessible.** S4, S5, S7, S9, S13, S14, S22, S23, S24, S25, S27, S28, S31 were all accessible and downloadable at review time.

**Label–link mismatches.** Several entries on the source page have labels that do not match the linked content:

- S9 is labeled as relating to event horizon topology but links to the Hawking memorial article (arXiv:2002.03185).
- S14 is labeled as "response of black holes to external fields" but links to a Raychaudhuri equation review (arXiv:gr-qc/0611123).
- S22 is labeled as "black holes as one-way valve" but links to a Klein–Gordon separation paper in Kerr–Newman (arXiv:1312.4823).
- S28 is labeled as "software injection" but links to a statistical GW data analysis review (arXiv:0711.1115).
- S30 links to arXiv:1304.0670 (observing scenarios), not to the GW150914 detection paper (arXiv:1602.03837).
- S31 is labeled as "computational horizons" but links to a broad gravitational wave survey (arXiv:2306.03797).

These mismatches likely reflect evolving draft labeling. Correcting them and adopting a consistent convention (publication year versus arXiv posting date) would improve usability.

### 5.3 Coverage Assessment

**Strengths.** The collection balances foundational texts with recent advances across a five-decade span. The mathematical emphasis—featuring rigorous treatments by Christodoulou, Chruściel, and Chandrasekhar alongside more accessible reviews by Teukolsky and Poisson—reflects the character of the field. The Kerr solution receives appropriately thorough coverage from multiple angles (historical, geometrical, perturbative). The scattering section preserves an important intellectual lineage from Matzner (1968) through the comprehensive monograph of Futterman, Handler, and Matzner (1988) to modern exact methods.

**Gaps.** Several areas relevant to the stated computational focus are underrepresented:

*Numerical relativity methods.* The collection contains no references on the 3+1 initial value formulation, gauge choices (BSSN, generalized harmonic), or the 2005–2006 breakthrough simulations. Works by Pretorius (2005), Campanelli et al. (2006), Baker et al. (2006), and the review by Baumgarte and Shapiro would strengthen the connection to computational practice. The Einstein Toolkit and related codebases (Cactus, Carpet, SpEC) are absent.

*Event horizon finding algorithms.* Despite the stated focus on computing event horizons, algorithmic references are missing. The methods of Thornburg for apparent horizon finding, backward null geodesic integration for event horizons, and the related computational geometry of crease-set tracking would directly support the computational goals.

*Quasi-normal modes.* While Teukolsky's review mentions QNMs and Chandrasekhar computes spectra in detail, the dedicated QNM literature—Leaver's continued fraction method, the comprehensive review by Berti, Cardoso, and Starinets, and recent work on QNM overtones—is absent. Given the central role of QNMs in ringdown analysis, this is a notable gap.

*Effective one-body formalism.* The Buonanno–Damour effective-one-body (EOB) approach, which bridges post-Newtonian theory and numerical relativity to produce complete inspiral-merger-ringdown waveforms, is not represented. EOB waveforms are the primary templates used in LIGO/Virgo analyses.

*Black hole thermodynamics beyond 1973.* The Hawking radiation derivation, the Bekenstein–Hawking entropy formula, the information paradox, and the Euclidean path integral approach to black hole thermodynamics are absent. While these lie somewhat outside the computational focus, they are central to the broader intellectual landscape.

*Wormholes.* The source page carries a "Worm holes" tag without corresponding bibliographic entries. If the scope extends to exotic solutions, the Morris–Thorne traversable wormhole paper and the ER=EPR conjecture would be natural additions. Otherwise, the tag should be removed.


## 6. Connections and Computational Context

### 6.1 Unifying Mathematical Structures

Several mathematical threads run through the entire collection, providing coherence beneath the four-section organization.

The **Raychaudhuri equation** appears explicitly in the area theorem (Section 1), the geodesic focusing that drives black hole formation (Section 1.3), the evolution of null generators on the event horizon (Section 2), and implicitly in the self-force program (Section 4.2) through its role in determining the evolution of the binary orbit. Understanding this single equation and its consequences is perhaps the most efficient entry point to the mathematical physics of black holes.

The **separability of wave equations in Kerr spacetime** connects Chandrasekhar's perturbation theory (Section 1.2) to Teukolsky's master equation (Section 1.4), the scattering calculations of Section 3, and the quasi-normal mode analyses underlying gravitational wave template construction (Section 4). The mathematical origin of this separability—the Killing tensor of the Kerr metric, discovered by Carter—is one of the deepest structural results in the theory.

**Null geodesics** are the geometric primitives throughout: they generate the event horizon (Section 2), determine scattering cross-sections (Section 3), and constitute the characteristics of the wave equations governing gravitational radiation (Section 4). The computational problem of black hole physics is, in a precise sense, the problem of tracking null geodesics in dynamical spacetimes.

### 6.2 Reading Paths

The collection supports several reading paths depending on the reader's goals:

*Mathematical foundations.* S3 (Wald) → S2 (Chandrasekhar) → S8 (Chruściel) → S4 (Christodoulou). This path develops the rigorous framework, progressing from the standard graduate treatment through exhaustive calculations of exact solutions to modern geometric methods and the formation problem.

*Computational black hole physics.* S3 (Wald, Chapters 10, 12) → S12 (Poisson toolkit) → S13 (Gourgoulhon–Jaramillo 3+1 null surfaces) → S14 (Raychaudhuri equation) → S10–11 (membrane paradigm). This path develops the formalism needed for numerical horizon finding and characterization.

*Gravitational wave physics.* S7 (Teukolsky) → S21 (Futterman–Handler–Matzner scattering) → S27 (Poisson–Pound–Vega self-force) → S28 (Jaranowski–Królak data analysis) → S30 (LIGO detection). This path follows the chain from perturbation theory through waveform modeling to observation.

*The Kerr solution.* S5 (Kerr discovery) → S6 (Wiltshire et al. monograph) → S7 (Teukolsky perturbations) → S2 (Chandrasekhar, Kerr chapters). This path provides a complete picture of the astrophysically relevant black hole solution.

### 6.3 Computational Projects

These notes provide framework for several computational projects that can be implemented in associated code repositories:

*Quasi-normal mode computation.* Using the Teukolsky equation (S7) and the spectral framework of Persides (S19–S20), implement a QNM solver via Leaver's continued fraction method or direct integration. Compare against tabulated values in Berti, Cardoso, and Starinets. The continued fraction method recasts the radial Teukolsky equation as a three-term recurrence relation for the expansion coefficients of the solution in a series of confluent hypergeometric functions; the QNM frequencies are the values of $\omega$ for which the continued fraction converges, which can be found by Newton's method in the complex $\omega$-plane. An alternative approach uses the WKB approximation, which gives QNM frequencies in terms of the peak and curvature of the effective potential—less accurate for low overtones but providing physical insight into the relationship between the QNM spectrum and the geometry of the photon sphere.

*Scattering cross-sections.* Implement the partial wave analysis of Matzner (S18) for scalar waves on a Schwarzschild background. Compute differential and total absorption cross-sections as a function of frequency. The partial wave expansion decomposes the scattering amplitude into contributions from each angular momentum mode $\ell$, with each mode governed by an ODE for the radial function. The phase shifts $\delta_\ell(\omega)$ determine the scattering matrix, and the cross-sections follow from standard scattering theory. At low frequencies ($M\omega \ll 1$), the absorption cross-section approaches the geometric area $27\pi M^2$ (the capture cross-section of the photon sphere). At high frequencies, the cross-section exhibits oscillatory behavior due to orbiting—waves that circle the photon sphere multiple times before escaping. Extend to the Kerr case using the Teukolsky formalism (S7), where superradiant scattering ($\omega < m\Omega_H$, with $\Omega_H$ the horizon angular velocity) provides an additional physical phenomenon to compute.

*Geodesic integration.* Compute null and timelike geodesics in Kerr spacetime, visualizing the photon sphere, the innermost stable circular orbit (ISCO), and plunging orbits. The fully integrable geodesic equations in Kerr spacetime (four constants of motion: $E$, $L_z$, $Q$, $\mu^2$) reduce to quadratures involving elliptic integrals, but direct numerical integration using a symplectic integrator is more flexible and allows visualization of general orbits including zoom-whirl behavior near the ISCO. Demonstrate frame dragging by comparing prograde and retrograde orbits, and illustrate the Penrose process by computing the energy of particles in the ergosphere. The geodesic structure of Kerr spacetime is also the foundation for ray-tracing codes that produce the images of black hole shadows now observed by the Event Horizon Telescope.

*Event horizon finding.* In the context of a numerically generated spacetime (or an analytic test case like Vaidya), implement backward null geodesic integration to locate the event horizon. The algorithm proceeds by seeding a family of outgoing null geodesics at late times (when the spacetime has settled to a Kerr solution and the horizon location is known analytically) and integrating backward in time. The geodesics that asymptotically approach the horizon trace out the event horizon surface. Crease points—where new generators join the horizon—require careful numerical treatment, as the null expansion diverges at these caustics. Compare with apparent horizon locations found from the marginally trapped surface equation, and quantify the difference between event and apparent horizons during the dynamical phase.

*Membrane paradigm diagnostics.* For a given black hole spacetime (Schwarzschild or Kerr), compute the membrane quantities: surface resistivity, shear viscosity, tidal fields. The membrane paradigm replaces the global structure of the black hole spacetime with boundary conditions on a timelike "stretched horizon" just outside the true horizon. For an external electromagnetic field $F_{ab}$, the induced surface current on the membrane satisfies Ohm's law with resistivity $4\pi/c = 377\,\Omega$ (in Gaussian units). This can be verified by computing the electromagnetic field of a test charge above a Schwarzschild black hole and evaluating the induced surface charge and current on the stretched horizon.

*Post-Newtonian orbital evolution.* Implement the post-Newtonian equations of motion for a binary system through at least 2.5PN order (where radiation reaction first enters) and compute the gravitational waveform during the inspiral phase. Compare the resulting waveform with the quadrupole formula, quantify the corrections from higher PN orders, and determine the frequency at which the PN approximation breaks down by comparison with numerical relativity results. This project bridges the self-force formalism of Section 4.2 with the data analysis methods of Section 4.3.


## 1. General theorems

| ID  | Link                                                                                                                                              | Notes                                                                                                              |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| S1  | [Hawking *“Blackhole mechanics”* 1973](https://www.worldscientific.com/doi/10.1142/9789812384935_0004?srsltid=AfmBOopaFDw-FhDDUU6zqXNNYi_LXe8i7J4SS2uLK71fysjr9PKr0GYd)      | Landmark work establishing the four laws of black hole mechanics and their deep analogy to thermodynamics.         |
| S2  | [Chandrasekhar *“Mathematical Theory of Blackholes”* 1983](https://global.oup.com/academic/product/the-mathematical-theory-of-black-holes-9780198503705?cc=us&lang=en&) | Rigorous mathematical treatment of exact black-hole solutions and their stability properties in general relativity. |
| S3  | [Wald *“General Relativity”* 1984](https://press.uchicago.edu/ucp/books/book/chicago/G/bo5952261.html)                                                | Authoritative graduate-level text covering the foundations of general relativity and the global theorems governing black holes. |
| S4  | [Christodoulou *“Formation of Black Holes in General Relativity”* 2008](https://arxiv.org/abs/0805.3880)                                              | Detailed proof demonstrating gravitational collapse in vacuum spacetimes leads to black-hole formation.             |
| S5  | [Kerr *“Discovering the solution”* 2008](https://arxiv.org/abs/0706.1109)                                                                             | Historical and technical overview of Roy Kerr’s derivation of the rotating black-hole metric.                     |
| S6  | [Wiltshire et al *“The Kerr Spacetime”* 2009](https://www.cambridge.org/us/universitypress/subjects/physics/theoretical-physics-and-mathematical-physics/kerr-spacetime-rotating-black-holes-general-relativity?format=HB&isbn=9780521885126#description) | Comprehensive monograph analyzing the geometry and physical properties of the Kerr solution.                       |
| S7  | [Teukolsky *“The Kerr Metric”* 2014](https://arxiv.org/abs/1410.2130)                                                                                  | Survey of perturbation theory and separability in Kerr spacetime for wave propagation analyses.                   |
| S8  | [Crusciel *“Geometry of Black holes”* 2020](https://global.oup.com/academic/product/geometry-of-black-holes-9780198855415?cc=us&lang=en)              | Mathematical exposition of black-hole geometry emphasizing horizon uniqueness theorems.                           |
| S9  | [Carr et al *“Stephen William Hawking CH CBE”* 2020](https://arxiv.org/pdf/2002.03185)                                                                  | Biographical and scientific overview summarizing Hawking’s key contributions to black-hole physics.               |


## 2. The event horizon

| ID   | Link                                                                                                                                                      | Notes                                                                                                                     |
|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| S10  | [Thorne et al *“Membrane paradigm”* 1986](https://www.science.org/doi/10.1126/science.234.4778.882.a)                                                        | Introduces the membrane paradigm, modeling the event horizon as a two-dimensional viscous surface with physical properties. |
| S11  | [Thorne et al *“Membrane paradigm”* 1986](https://inspirehep.net/literature/268144)                                                                          | Extended discussion of horizon electrodynamics and fluid analogies within the membrane framework.                          |
| S12  | [Poisson *“A Relativist's Toolkit”* 2004](https://www.cambridge.org/core/books/relativists-toolkit/DA7ED68B971708A0F782257F948981E7) | A modern text including detailed consideration of null surfaces, with a detailed derivation of horizon boundary conditions.                     |
| S13  | [Gourgoulhon and Jaramillo *“3+1 perspective on null surfaces”* 2005](https://arxiv.org/abs/gr-qc/0503113)                                                                     | Applies a 3+1 decomposition to characterize the geometry and evolution of null hypersurfaces such as event horizons.        |
| S14  | [Kar and SenGupta *“Raychaudhuri equations”* 2007](https://arxiv.org/abs/gr-qc/0611123)                                                                         | Derives Raychaudhuri’s equation in various geometric settings to analyze horizon focusing and caustic formation.           |
| S15  | [Emparan and Martínez *“Black hole fusion”* 2016](https://www.worldscientific.com/doi/10.1142/S0218271816440156?srsltid=AfmBOootwmIeX_9Vj22zPrJjZ-1UJcLasrf6jhhJulOiGTmQbITMh3Am)     | Studies the dynamics of event horizons during black-hole mergers in higher-dimensional spacetimes.                         |
| S16  | [Emparan et al *“Black hole fusion in the extreme mass ratio”* 2018](https://arxiv.org/abs/1708.08868)                                                        | Numerical investigation of horizon deformation in extreme-mass-ratio inspirals.                                            |
| S17  | [Gadioux *“Evolution of creases on the event horizon”* 2024](https://arxiv.org/abs/2407.07962)                                                                 | Examines the formation and evolution of crease sets on dynamical horizons during non-linear interactions.                  |


## 3. Scattering from black holes

| ID   | Link                                                                                                                                                                | Notes                                                                                                        |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| S18  | [Matzner *“Scattering from Blackholes”* 1968](https://pubs.aip.org/aip/jmp/article-abstract/9/1/163/233956/Scattering-of-Massless-Scalar-Waves-by-a?redirectedFrom=fulltext) | Early analysis of massless scalar wave scattering by a Schwarzschild black hole, establishing cross-sections. |
| S19  | [Persides *“Laplacian on Schwarzschild”* 1973](https://www.sciencedirect.com/science/article/pii/0022247X73902771)                                                      | Investigates spectral properties of the Laplace operator on the Schwarzschild background.                    |
| S20  | [Persides *“Radial Schwarzschild”* 1973](https://pubs.aip.org/aip/jmp/article-abstract/14/8/1017/453022/On-the-radial-wave-equation-in-Schwarzschild-s?redirectedFrom=fulltext)    | Derives and analyzes the radial wave equation governing scattering in Schwarzschild spacetime.               |
| S21  | [Futterman et al *“Scattering from black holes”* 1988](https://www.cambridge.org/core/books/scattering-from-black-holes/1119267BC3D50792E67F4176AA74006B#fndtn-information)  | Comprehensive monograph covering quantum and classical wave scattering by black holes across spin fields.  |
| S22  | [Bezzerra *“Scattering from charge and rotating black holes”* 2013](https://arxiv.org/abs/1312.4823)                                                                     | Extends scattering theory to charged (Reissner–Nordström) and rotating (Kerr) black-hole backgrounds.        |
| S23  | [Li et al *“Exact Scattering”* 2022](https://arxiv.org/abs/1612.02644)                                                                                                  | Presents exact analytic solutions for wave scattering in certain black-hole geometries.                     |


## 4. Gravitational waves

| ID   | Link                                                                                                                                                                                               | Notes                                                                                                                   |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| S24  | [Trimble and Thorne *“Binaries”* 2018](https://arxiv.org/abs/1811.04310)                                                                                                                               | Review of binary black-hole dynamics and their astrophysical and gravitational-wave implications.                     |
| S25  | [Quinn *“Radiating scalar particle”* 2000](https://arxiv.org/abs/gr-qc/0005030)                                                                                                                      | Analyzes the self-force and radiation reaction of a scalar charge in curved spacetime.                                  |
| S26  | [de Felice and Bini *“Classical Measurement in Curved Spacetime”* 2010](https://www.cambridge.org/core/books/classical-measurements-in-curved-spacetimes/DAA20E1188767CB570A4A0C60BA91485#fndtn-information) | Develops a formalism for how classical observers measure tidal and radiative effects in curved backgrounds.            |
| S27  | [Posisson *“The radiating particle”* 2011](https://link.springer.com/content/pdf/10.12942/lrr-2011-7.pdf)                                                                                             | Reviews motion and self-force of point particles emitting gravitational radiation in general relativity.               |
| S28  | [Jaranowski and Królak *“Gravitational-wave data”* 2023](https://arxiv.org/abs/0711.1115)                                                                                                             | Survey of statistical and computational methods for analyzing and interpreting gravitational-wave signals.               |
| S29  | [Romano and Cornish *“Stochastic gravitational wave backgrouns”* 2017](https://arxiv.org/abs/1608.06889)                                                                                              | Reviews theoretical models and detection strategies for stochastic gravitational-wave backgrounds.                      |
| S30  | [LIGO et al *“Gravitational Waves”* 2020](https://arxiv.org/abs/1304.0670)                                                                                                                           | Landmark LIGO/Virgo collaboration report presenting the first direct detection of gravitational waves from a binary merger. |
| S31  | [Pretorius *“Survey of Gravitational Waves”* 2023](https://arxiv.org/abs/2306.03797)                                                                                                                 | Comprehensive overview of numerical relativity simulations and observational prospects in gravitational-wave astronomy. |
