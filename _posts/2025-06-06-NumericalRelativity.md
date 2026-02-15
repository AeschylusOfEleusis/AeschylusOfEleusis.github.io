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

## 1. Introduction

Einstein's field equations, $G_{\mu\nu} = 8\pi T_{\mu\nu}$, encode the nonlinear
dynamics of spacetime geometry coupled to matter and energy. In their full
generality, these ten coupled partial differential equations admit no
closed-form solutions for most physically interesting configurations---binary
black hole mergers, neutron star collisions, gravitational collapse near
criticality. Numerical relativity is the enterprise of solving Einstein's
equations on computers, and the story of how that enterprise developed is
the story of how several distinct intellectual threads---finite difference
theory, constrained evolution of hyperbolic systems, adaptive mesh refinement,
and careful mathematical analysis of horizons and singularities---were
woven together over roughly six decades.

The difficulty of this enterprise is worth emphasizing at the outset. The
Einstein equations are not merely nonlinear; they are nonlinear in a way
that involves the structure of spacetime itself. The equations describe how
matter tells spacetime to curve and how spacetime tells matter to move, but
the equations themselves must be solved *on* the spacetime they determine.
There is no fixed background on which to compute---the computational domain
is itself a dynamical quantity. This feature distinguishes numerical relativity
from most other computational physics: in fluid dynamics, one solves for the
fluid on a fixed spatial domain; in numerical relativity, one must
simultaneously determine the solution *and* the spacetime on which it lives.

The practical consequences are profound. Coordinate choices that work well
in one region of spacetime may become singular in another. Gauge conditions
(the relativistic analog of coordinate choices) must be imposed dynamically
during evolution, and poor choices can crash a simulation even when the
underlying physics is perfectly regular. The constraints of general
relativity---the Hamiltonian and momentum constraints, which are the
relativistic analogs of the divergence equations in electromagnetism---must
be satisfied on every time slice, but numerical errors in the evolution
tend to violate them. Managing this constraint violation, either by
damping it or by reformulating the equations to make violation less
catastrophic, consumed much of the field's intellectual energy for
three decades.

These notes trace the development of the field through its literature. The
treatment is organized around four principal themes: the discretization of
continuum equations (Section 2), the reformulation of Einstein's equations
into computationally tractable form and the community infrastructure built
to solve them (Section 3), gravitational collapse and the discovery of
critical phenomena (Section 4), and the problem of locating black hole
horizons in numerically evolved spacetimes (Section 5). A final section
identifies significant gaps in the present coverage and sketches directions
for future development.

The selection of references is deliberately idiosyncratic. It emphasizes
foundational algorithmic papers that shaped how the field thinks about
computation, seminal physical discoveries that numerical methods made possible,
and modern open-source infrastructure that defines contemporary practice.
Many important topics---spectral methods, finite-volume schemes for
relativistic hydrodynamics, gravitational wave extraction, the
breakthrough binary black hole simulations of 2005--2006---receive only
passing mention here. This reflects the present state of a living document,
not a judgment about their importance.

A word about prerequisites. The reader is assumed to have working familiarity
with general relativity at the level of Carroll or Wald, partial differential
equations at the level of a standard graduate course, and some experience
with numerical computation. Where the discussion touches on topics that
require more specialized background---the conformal decomposition of the
Einstein constraints, say, or the theory of marginally trapped surfaces---I
have tried to provide enough context for the main ideas to be followed, with
pointers to the literature for the details.

Throughout, reference numbers of the form S*n* refer to the annotated
bibliography at the end of this chapter.


## 2. Discretizing the Continuum

### 2.1 Richardson and the origins of finite differences

The systematic application of finite-difference methods to differential
equations begins, for practical purposes, with Lewis Fry Richardson's 1910
paper in the *Philosophical Transactions of the Royal Society* [S1].
Richardson introduced what would become known as Richardson extrapolation:
given numerical solutions computed at two different grid spacings $h$ and
$h/2$, one can combine them to cancel the leading-order truncation error
and obtain a result of higher effective order. The idea is simple. If a
numerical scheme has error $E(h) = c \, h^p + O(h^{p+1})$, then the
combination

$$
f_{\text{ext}} = \frac{2^p f(h/2) - f(h)}{2^p - 1}
$$

eliminates the $O(h^p)$ term, yielding an approximation accurate to $O(h^{p+1})$.

This technique remains fundamental. In modern numerical relativity,
convergence testing---running simulations at multiple resolutions and
checking that the Richardson-extrapolated error converges at the expected
rate---is the primary tool for code verification. When a numerical relativity
group reports that their binary black hole waveforms exhibit fourth-order
convergence, they are performing a direct descendant of Richardson's procedure
on a system whose complexity Richardson could not have imagined.

### 2.2 Early computational fluid dynamics: DeWitt

Bryce DeWitt's papers on Lagrangian hydrodynamics from the early 1950s
[S2, S3] document computational methods developed in the postwar period,
often in connection with weapons research at the national laboratories.
The Lagrangian approach to fluid dynamics follows individual fluid parcels
rather than monitoring fixed spatial locations (the Eulerian approach). This
distinction---Lagrangian versus Eulerian---reappears throughout computational
physics and has direct consequences for numerical relativity. When matter
is coupled to spacetime evolution, codes must choose how to represent both
the fluid and the geometry, and the choice between Lagrangian and Eulerian
descriptions of the matter has significant implications for accuracy near
shocks, conservation properties, and computational cost.

DeWitt would later become one of the most important figures in quantum
gravity, but this early numerical work illustrates a recurring theme: the
cross-pollination between applied computational physics and fundamental
theory. People who learned to compute in weapons programs carried
algorithmic sensibilities into general relativity, and the computational
infrastructure of the field bears the imprint of that lineage.

### 2.3 Stability and accuracy for hyperbolic systems: Kreiss and Oliger

The Einstein evolution equations, once cast into first-order-in-time form
via the 3+1 decomposition (Section 3), constitute a system of hyperbolic
partial differential equations. The stability and accuracy of
finite-difference approximations to hyperbolic systems was the subject
of intensive study in the 1970s, and the collaboration between Heinz-Otto
Kreiss and Joseph Oliger produced foundational results that directly
informed the design of early numerical relativity codes.

Their 1972 comparison paper [S4] systematically evaluated finite-difference
schemes for hyperbolic equations, establishing benchmarks for accuracy and
computational efficiency. The 1973 monograph on time-dependent problems
[S5] became a standard reference for stability analysis, particularly the
energy method approach to establishing well-posedness of the semidiscrete
system. In practice, the "Kreiss--Oliger" name is most strongly associated
with the addition of controlled high-order numerical dissipation to
stabilize evolution schemes. The idea is to add a small amount of
artificial dissipation, scaled to act primarily at the grid scale, that
damps high-frequency numerical noise without significantly affecting the
resolved physics. For a fourth-order accurate scheme, one adds a
sixth-order dissipation operator:

$$
Q_{\text{KO}} = (-1)^{(r+1)/2} \epsilon \, (\Delta x)^r \, D_+^{r/2} D_-^{r/2}
$$

where $r$ is the order of dissipation, $D_+$ and $D_-$ are forward and
backward difference operators, and $\epsilon$ is a tunable coefficient.
This technique is used routinely in modern BSSN evolution codes.

Abarbanel, Gottlieb, and Turkel's 1975 SIAM paper [S6] extended this
program to fourth-order accurate schemes for hyperbolic equations. The
practical point is that higher-order methods can achieve a given accuracy
target with coarser grids, reducing computational cost---a consideration
that becomes critical when each grid point carries dozens of evolved
variables (as in the BSSN system) and the domain must resolve length scales
spanning several orders of magnitude.

### 2.4 Adaptive mesh refinement

The single most consequential algorithmic development for numerical
relativity is, arguably, adaptive mesh refinement (AMR). The Berger--Oliger
algorithm, introduced in their 1984 paper [S8], addresses a fundamental
challenge in solving hyperbolic PDEs: solutions often develop localized
features---shock fronts, wave crests, the strong-field region near a
black hole---while large portions of the computational domain remain
smooth and require far less resolution.

The key insight is to dynamically create and destroy refined grid patches
based on local error estimates. The algorithm operates recursively: a
coarse base grid covers the entire domain, and refined subgrids (with mesh
spacing reduced by integer factors, typically 2 or 4, in both space and
time) are created wherever the estimated truncation error exceeds a
threshold. These refined grids can themselves contain even finer grids,
producing a hierarchy of nested patches. Richardson-type error estimates
drive the refinement decisions, directly connecting the 1910 technique to
modern adaptive computation.

For binary black hole simulations, AMR is not merely convenient but
essential. The strong-field dynamics near each horizon require resolution
on the scale of the black hole mass $M$, while gravitational waves must be
extracted at distances of order $100M$ or more from the source. Without
AMR, resolving both regions simultaneously would require uniform grids with
$10^{12}$ or more points in three dimensions---far beyond any foreseeable
computational resource.

Berger and Colella's 1989 extension [S9] introduced block-structured grids,
improving efficiency for multidimensional problems. Rather than refining
individual cells, the algorithm groups nearby cells requiring refinement
into rectangular patches, allowing efficient array-based computation on
each patch. This approach underlies both major AMR implementations in
current numerical relativity: the Carpet driver used in the Einstein
Toolkit, and the Chombo library underlying GRChombo.

A key technical detail deserves attention: the treatment of coarse-fine
grid boundaries. When a refined grid is embedded in a coarser grid,
the two grids must exchange data at their shared boundaries. The fine
grid receives boundary data by interpolating from the coarse grid
(prolongation), and the coarse grid receives updated data from the fine
grid where the fine grid has evolved to a more advanced time
(restriction). For conservation laws, an additional "refluxing" step
corrects the coarse-grid fluxes at the boundary to ensure that the
total conserved quantity is consistent across refinement levels. In
numerical relativity, the evolved quantities are not conserved in the
traditional sense (the BSSN system does not have a conservation-law
structure), but careful treatment of prolongation and restriction
operators remains essential for stability and convergence.

The interpolation order at coarse-fine boundaries must be compatible
with the order of the evolution scheme. A fourth-order evolution scheme
paired with second-order prolongation will produce reflections and
constraint-violating modes at refinement boundaries. This mismatch was
a source of significant difficulties in early AMR implementations for
numerical relativity and required careful engineering to resolve.

The intellectual arc from Richardson (1910) through Kreiss--Oliger (1972--1975)
to Berger--Oliger (1984) to Berger--Colella (1989) constitutes a remarkably
coherent development. Each generation built directly on the preceding one:
Richardson's error estimation enables Kreiss and Oliger's stability-aware
discretization, which in turn enables Berger and Oliger's adaptive algorithm,
which Berger and Colella then make practical for multidimensional problems.
The reader interested in numerical relativity inherits this entire chain.


## 3. Formalisms, Infrastructure, and the Road to Binary Black Holes

### 3.1 The 3+1 decomposition

Einstein's equations are written covariantly in four-dimensional spacetime,
but computation requires specifying what is "space" and what is "time."
The 3+1 (or ADM) decomposition, developed by Arnowitt, Deser, and Misner
in the late 1950s and early 1960s, accomplishes this by foliating spacetime
into a family of spacelike hypersurfaces $\Sigma_t$ parameterized by a
time coordinate $t$. The spacetime metric is decomposed as

$$
ds^2 = -\alpha^2 \, dt^2 + \gamma_{ij}(dx^i + \beta^i \, dt)(dx^j + \beta^j \, dt)
$$

where $\alpha$ is the lapse function (controlling the rate of proper time
advance between slices), $\beta^i$ is the shift vector (controlling how
spatial coordinates propagate from slice to slice), and $\gamma_{ij}$ is
the induced three-metric on each slice. The extrinsic curvature
$K_{ij}$, measuring how each slice is embedded in the four-dimensional
spacetime, serves as the conjugate momentum to $\gamma_{ij}$.

Einstein's equations decompose into two classes: constraint equations
(the Hamiltonian and momentum constraints) that must be satisfied on
each slice, and evolution equations that propagate $\gamma_{ij}$ and
$K_{ij}$ from one slice to the next. The constraints are analogous to
the divergence equations in electromagnetism---they constrain the initial
data but are (in principle) preserved by the evolution.

The ADM formulation, while conceptually clean, proves numerically unstable.
The evolution equations, as written by ADM, are only weakly hyperbolic,
meaning that small perturbations can grow without bound and crash the
simulation. The history of numerical relativity from the 1960s through
the early 2000s is, in significant part, the history of reformulating
the ADM equations into strongly hyperbolic systems that admit stable
numerical evolution.

Two reformulations dominate current practice. The BSSN formulation
(Baumgarte--Shapiro--Shibata--Nakamura) performs a conformal decomposition
of the spatial metric, $\gamma_{ij} = e^{4\phi} \tilde{\gamma}_{ij}$ with
$\det \tilde{\gamma}_{ij} = 1$, and introduces auxiliary variables that
promote certain constraint-related quantities to independently evolved
fields. The conformal factor $\phi$ absorbs the determinant of the metric,
the conformal connection functions $\tilde{\Gamma}^i = \tilde{\gamma}^{jk}
\tilde{\Gamma}^i_{jk}$ are promoted to independently evolved variables (rather
than being computed from derivatives of the metric), and the trace of the
extrinsic curvature $K$ is evolved separately from the traceless part
$\tilde{A}_{ij} = e^{-4\phi}(K_{ij} - \frac{1}{3}\gamma_{ij}K)$.

The promotion of the $\tilde{\Gamma}^i$ to evolved variables is the key
step that distinguishes BSSN from ADM. In the ADM formulation, the
connection functions are derivatives of the metric---they are not
independent variables. By treating them as independent and adding their
evolution equation (derived from the original system), the BSSN
formulation modifies the principal part of the evolution system in a way
that renders it strongly hyperbolic for appropriate gauge choices. The
mathematical mechanism is subtle: the auxiliary variable introduction
changes the constraint propagation system, ensuring that constraint
violations are damped rather than amplified during evolution.

Combined with the "1+log" slicing condition for $\alpha$,

$$
(\partial_t - \beta^i \partial_i) \alpha = -2\alpha K,
$$

and the "Gamma-driver" condition for $\beta^i$,

$$
\partial_t \beta^i = \frac{3}{4} \tilde{\Gamma}^i - \eta \beta^i,
$$

BSSN achieves robust long-term stability. The 1+log condition is
singularity-avoiding: as a region of spacetime approaches a singularity
($K \to \infty$), the lapse $\alpha$ is driven toward zero, freezing the
evolution in that region. The Gamma-driver shift condition minimizes
coordinate distortion during evolution, a property sometimes described
as "almost-Killing" gauge. The damping parameter $\eta$ controls how
quickly the shift responds to changes in the conformal connection.

The generalized harmonic formulation, used by Pretorius in his
2005 breakthrough, takes a different approach. It imposes harmonic-type
gauge conditions at the level of the equations of motion by requiring that
the gauge source functions $H_\mu = \square x_\mu$ satisfy prescribed
evolution equations. This yields a manifestly hyperbolic system (the
reduced Einstein equations take the form of a set of curved-space wave
equations for the metric components), with well-posedness following from
standard results for quasilinear wave equations. Constraint damping---the
addition of terms proportional to the constraints to the evolution
equations---ensures that numerical constraint violations are exponentially
damped during evolution.

The two textbooks cited in the annotated bibliography---Baumgarte and
Shapiro [S11] and Shibata [S15]---provide complementary treatments of
this material. Baumgarte and Shapiro develop the theory alongside numerical
implementation considerations, reflecting both authors' experience
combining analytical and computational approaches. Their treatment of
the BSSN system (which Baumgarte co-developed) is naturally authoritative.
Shibata's text emphasizes practical implementation details drawn from
extensive simulation experience, with particular strength in
matter-coupled evolution (relativistic hydrodynamics and magnetohydrodynamics),
gravitational wave extraction, and end-to-end simulation workflows. Together,
these two books supply the theoretical backbone that connects the numerical
methods of Section 2 to the physical applications of Sections 4 and 5.

### 3.2 The first binary black hole simulation

Larry Smarr and collaborators' 1976 paper [S10] represents a landmark: one
of the first numerical simulations of colliding black holes. Working in
axisymmetry with head-on collisions, they demonstrated that Einstein's
equations could be evolved numerically through the highly nonlinear merger
phase. The simulation confirmed theoretical expectations for gravitational
wave emission during collision and established the feasibility of numerical
relativity for gravitational wave source modeling.

The gap between Smarr's 1976 simulation and the achievement of stable
binary black hole orbits in 2005---nearly three decades---testifies to the
difficulty of the problem. The obstacles were not primarily computational
(though Moore's law certainly helped) but rather mathematical and
algorithmic: finding evolution formalisms, gauge conditions, and boundary
treatments that maintained stability over the dozens of orbits required to
model an astrophysically realistic inspiral. This gap is worth dwelling on.
It illustrates that in computational science, raw computing power is
necessary but rarely sufficient; the algorithms and mathematical formulations
matter at least as much.

### 3.3 The 2005--2006 breakthroughs

Although the breakthrough papers are not individually listed in the
present bibliography (an acknowledged gap), no account of numerical
relativity can omit them. In 2005, Frans Pretorius achieved the first
stable simulation of a binary black hole inspiral, merger, and ringdown
using a generalized harmonic formulation with constraint damping and
adaptive mesh refinement. Almost immediately, two groups---Baker,
Campanelli, and collaborators, and Campanelli, Lousto, Marronetti, and
Zlochower---demonstrated that the BSSN formulation with moving puncture
gauge conditions could achieve comparable results with a conceptually
simpler approach. These three papers transformed numerical relativity
from a field that had struggled for decades with stability to one
producing routine, high-accuracy waveforms within a few years.

The moving puncture approach proved particularly influential because of
its simplicity: it requires no explicit excision of the black hole
interior and works with standard Cartesian AMR grids. The gauge conditions
that make it work---1+log slicing and Gamma-driver shift---had been studied
for years, but their effectiveness in the binary context was not fully
appreciated until the breakthrough simulations demonstrated it empirically.

### 3.4 Community infrastructure

The transition from isolated group codes to community-developed, open-source
infrastructure represents a paradigm shift in how numerical relativity
research is conducted. Two major platforms exemplify this transformation.

**The Einstein Toolkit** [S12] is built around the Cactus computational
framework, which provides a modular architecture for organizing physics
codes into independently developed components called "thorns." The Carpet
driver implements block-structured adaptive mesh refinement following the
Berger--Colella approach. The McLachlan thorn implements BSSN evolution
with constraint damping, generated automatically from tensor equations
using the Kranc code-generation package. General-relativistic
hydrodynamics capabilities, comprehensive analysis tools for gravitational
wave extraction, and standardized test suites complete the ecosystem.

By 2011, the Einstein Toolkit collaboration reported approximately 7,000
core-years of computing time used annually across more than a dozen
research groups, with over 90 peer-reviewed publications. The toolkit's
significance extends beyond its technical capabilities: by establishing
community standards for code verification (convergence testing, standard
test problems), it raised the bar for the entire field.

**GRChombo** [S13], built on the Chombo AMR library from Lawrence Berkeley
National Laboratory, emphasizes full adaptive mesh refinement capabilities
with block-structured Berger--Rigoutsos grid generation. It implements
both BSSN and the CCZ4 (conformal and covariant Z4) formulation, which
incorporates algebraic constraint damping directly into the evolution
system. The key technical distinction from the Einstein Toolkit is
GRChombo's support for "many-boxes-in-many-boxes" mesh hierarchies and
its dimension-independent core, which permits numerical experiments in
up to six spatial dimensions. This capability enables study of problems
with dynamically generated length scales---nonlinear instabilities of
black holes in higher dimensions, cosmological bubble collisions, scalar
field collapse near criticality---while maintaining fourth-order
convergence on standard test cases.

The existence of two mature, independently developed frameworks with
different design philosophies is itself valuable: it enables cross-code
verification, where the same physical problem is solved by different
codes and the results compared. Agreement between codes with different
formulations, discretizations, and AMR strategies provides confidence
that the results are physical rather than numerical artifacts.

### 3.5 Surveys and perspectives

Several broad reviews complement the textbooks and infrastructure papers.
Choptuik, Lehner, and Pretorius [S14] survey methods and results for
investigating strong-field gravitational dynamics through high-resolution
numerical simulations, emphasizing how numerical relativity enables
exploration of regimes inaccessible to perturbation theory. Scheel and
Thorne [S16] survey discoveries in geometrodynamics---the nonlinear
dynamics of curved spacetime---enabled by numerical simulations. Their
review introduces the tendex/vortex visualization framework for
understanding spacetime dynamics and connects numerical relativity to
gravitational wave detection through LIGO. The Simulating eXtreme
Spacetimes (SXS) collaboration, which Scheel leads, has produced the most
accurate binary black hole waveforms for LIGO data analysis. Thorne's
involvement directly connects the computational enterprise to the
observational program that vindicated it.

Varma's Caltech PhD thesis [S17] demonstrates a different kind of
connection between numerical relativity and observation: surrogate models
trained on high-fidelity numerical simulations can be evaluated in
fractions of a second on consumer hardware, enabling the rapid waveform
evaluation required for Bayesian parameter estimation in gravitational
wave data analysis. It is important to be precise about what this achieves:
the full Einstein-equation evolution still requires supercomputer resources;
what runs on a laptop is a carefully trained interpolant over the space of
parameters and waveforms. The distinction matters because the surrogate's
fidelity depends entirely on the quality and coverage of the underlying
numerical simulations.

Finally, Gorard's 2021 paper [S18] on the Cauchy problem in general
relativity formulated through the Wolfram physics model represents an
entry from outside mainstream numerical relativity. The Wolfram model
posits discrete structures underlying spacetime; Gorard attempts to
connect this framework to established initial value formulations of
general relativity. Whether this approach will prove productive remains
to be seen. Its inclusion here reflects a general openness to
alternative computational paradigms, with the caveat that readers should
evaluate it against the substantial body of well-posedness results and
constraint-control analyses that underpin standard formulations.


## 4. Gravitational Collapse and Critical Phenomena

### 4.1 The discovery

Matt Choptuik's 1993 *Physical Review Letters* paper [S19] stands among
the most important results in numerical relativity, and it provides a
particularly clear example of numerical computation revealing genuinely
new physics. Studying the spherically symmetric collapse of a massless
scalar field, Choptuik observed remarkable behavior at the threshold of
black hole formation.

The setup is deceptively simple. Consider a one-parameter family of
initial data for a massless scalar field in spherical symmetry, where
the parameter $p$ controls the "strength" of the initial pulse. For
small $p$, the pulse disperses to infinity. For large $p$, a black hole
forms. What happens at the critical value $p^*$ separating these two
outcomes?

Choptuik's numerical experiments, performed with extraordinary precision
using adaptive mesh refinement, revealed three properties of the critical
solution:

*Power-law scaling.* The mass of black holes formed just above threshold
follows $M \sim |p - p^*|^\gamma$ where $\gamma \approx 0.37$ is
independent of the choice of initial data family. This universality of
the critical exponent, shared across different parameterizations of the
initial data, was the first surprise.

*Discrete self-similarity.* The critical solution (obtained in the limit
$p \to p^*$) exhibits a discrete self-similarity: it is periodic in
logarithmic time with an echoing period $\Delta \approx 3.44$. That is,
the solution repeats its structure at geometrically decreasing scales, with
each "echo" a factor of $e^\Delta \approx 31$ smaller than the last.

*Universality.* Different one-parameter families of initial data, tuned
to their respective critical values, all approach the same critical
solution. The critical solution is an attractor of codimension one in the
space of initial data, with exactly one unstable mode. Initial data slightly
above $p^*$ follow the critical solution for many echoing cycles before
deviating toward black hole formation; data slightly below $p^*$ follow
it equally long before dispersing.

The parallels to critical phenomena in statistical mechanics are deep and
precise. The critical solution plays the role of a fixed point of the
renormalization group; the single unstable mode corresponds to the relevant
eigenvalue; the mass scaling exponent $\gamma$ is a critical exponent in
the Kadanoff--Wilson sense. The universality classes---determined by the
matter model and spacetime symmetries rather than by initial data
details---parallel universality classes in condensed matter physics. These
connections were not merely analogical; they could be made rigorous through
the dynamical systems formulation of the critical collapse problem.

The dynamical systems picture works as follows. Consider the space of all
initial data sets for the Einstein--scalar-field system, modulo the
symmetries of the system. This is an infinite-dimensional function space.
The time evolution defines a flow on this space. The critical solution
$Z^*$ is a fixed point of this flow (more precisely, a periodic orbit for
DSS or a fixed point for CSS systems). The linearized flow around $Z^*$
has exactly one eigenvalue $\lambda_0$ with positive real part (the unstable
mode), with the remaining spectrum in the left half-plane (the stable modes).
The critical surface---the set of initial data that flow asymptotically to
$Z^*$---has codimension one, separating the basins of attraction for
dispersal and black hole formation.

Near the critical surface, a generic one-parameter family of initial data
crosses the surface transversally at $p = p^*$. For $|p - p^*|$ small, the
data spends a long "time" (in the appropriate logarithmic variable) near
$Z^*$ before deviating toward the endpoint. The scaling law
$M \sim |p - p^*|^\gamma$ follows from this picture, with
$\gamma = 1/\lambda_0$ where $\lambda_0$ is the unstable eigenvalue of
the critical solution. The universality of $\gamma$---its independence
from the choice of initial data family---follows from the fact that it
depends only on $Z^*$ and its perturbation spectrum, not on the particular
path through the space of initial data.

### 4.2 Extensions in lower dimensions

Pretorius and Choptuik [S20] extended the critical collapse program to
(2+1)-dimensional spacetime, where gravity has no local propagating
degrees of freedom but retains global topological structure. The lower
dimensionality serves as a theoretical laboratory: by studying how
critical phenomena manifest in a simplified setting, one gains insight
into which features are dimension-dependent and which are universal
in a stronger sense.

The 2+1 setting introduces qualitative differences. With a negative
cosmological constant (as required for black hole formation in 2+1
dimensions, where the BTZ solution plays the role of the Kerr solution),
the critical solution's structure and the scaling exponent differ from
the 3+1 case. The work also provides a concrete example of singularity
excision techniques: since collapse proceeds to a singularity, the
numerical domain must be truncated before the singularity forms,
requiring careful treatment of the excision boundary.

Jałmużna, Gundlach, and Chmaj [S22] revisited scalar field critical
collapse in 2+1 dimensions with improved numerical resolution, enabling
more precise determination of critical exponents and investigation of
fine structure in the self-similar solution. Their work illustrates a
recurring pattern in computational science: increasing computational
resources permit refinement of earlier results, but the refinement often
reveals subtleties---in this case, questions about differentiability and
regularity at matching surfaces that affect mode structure and the
inferred universality class.

### 4.3 The living review

Gundlach and Martín-García's *Living Reviews in Relativity* article [S21]
provides the definitive survey of critical phenomena in gravitational
collapse as of 2007. For anyone entering this subject, it is the natural
first stop. The review develops the dynamical systems formulation
systematically, distinguishes between continuous and discrete
self-similarity (CSS and DSS), classifies transitions as Type I
(discontinuous, where the critical solution is a metastable star or
black hole) or Type II (continuous, where the critical solution is
self-similar and the black hole mass scales continuously to zero), and
catalogs critical exponents for various matter models and spacetime
dimensions.

The review also addresses the connection to cosmic censorship: critical
solutions produce naked singularities visible to distant observers, but
only as a set of measure zero in the space of initial data. This is
consistent with the weak cosmic censorship conjecture, which posits that
naked singularities do not form from "generic" initial data---though
defining "generic" precisely enough to prove the conjecture remains an
open problem.

### 4.4 Higher dimensions and cosmic censorship

Figueras and collaborators' study [S23] of the Gregory--Laflamme
instability endpoint shifts the setting from astrophysical 3+1
numerical relativity to higher-dimensional gravity. The Gregory--Laflamme
instability, discovered in 1993, shows that black strings---black holes
with horizon topology $S^2 \times S^1$ extended along a compact extra
dimension---become unstable to pinching perturbations above a critical
wavelength. The natural question is: what is the endpoint of this
instability?

The numerical results are striking. The evolution proceeds through a
cascade of spherical black holes connected by increasingly thin
string-like necks at multiple scales, with no single global timescale
relating successive generations. The endpoint is horizon pinch-off in
finite asymptotic time, forming a naked singularity. This result
confirms violation of weak cosmic censorship in these higher-dimensional
spacetimes, demonstrating that pathological configurations can form from
smooth initial data through dynamical evolution.

The cascade structure is itself remarkable from a computational perspective.
Each successive generation of necks forms at a smaller length scale than
the preceding one, requiring the AMR hierarchy to adapt dynamically to
resolve features that did not exist in the initial data. The simulations
require resolution spanning many orders of magnitude, sustained over
evolution times long enough for multiple generations of neck formation. This
is a problem for which full AMR is genuinely essential, not merely convenient.

From a numerical methods perspective, the problem demands the full
capabilities of modern AMR infrastructure (dynamically generated length
scales spanning many orders of magnitude), higher-dimensional evolution
codes (GRChombo's dimension-independent core is directly relevant here),
and careful convergence testing to distinguish physical pinch-off from
numerical artifacts. The result is a compelling demonstration of
numerical relativity as a tool for mathematical physics, not merely
astrophysical simulation.

### 4.5 Connections to the broader program

The critical phenomena and cosmic censorship themes in this section connect
to broader questions in mathematical physics that run through several
chapters of this book. The universality and scaling behavior discovered by
Choptuik bear a mathematical kinship to renormalization group ideas in
quantum field theory (treated elsewhere in these notes). The
infinite-dimensional dynamical systems framework that explains critical
collapse parallels the path integral formulations that appear in both
quantum field theory and computational finance. The discrete self-similarity
of the Choptuik solution---a symmetry under rescaling by a fixed
factor---is a discrete analog of the continuous scale invariance that
appears at critical points in statistical mechanics and in conformal
field theories.

These connections are not accidental. They reflect the deep mathematical
unity of apparently disparate physical theories, mediated by shared
structures: renormalization group flows, attractors in function spaces,
scaling limits. The reader who has worked through the quantum field theory
or computational finance chapters will find familiar mathematical machinery
appearing in an entirely different physical context.


## 5. Finding Horizons

### 5.1 Event horizons and apparent horizons

The problem of locating black hole boundaries in numerically evolved
spacetimes is both practically essential and conceptually subtle. Two
distinct mathematical objects are in play, and the distinction between
them has significant computational consequences.

The *event horizon* is the boundary of the black hole region: the set
of events from which no future-directed causal curve can reach future
null infinity. It is defined by global causal structure---one must know
the entire future evolution of the spacetime to determine which events
are inside the event horizon and which are outside. This makes event
horizons fundamentally nonlocal in time: they can only be found after
a simulation completes (or, more precisely, after enough of the future
evolution is known to determine the causal structure in the region of
interest).

The *apparent horizon* is a local concept: it is the outermost marginally
trapped surface on a given spatial slice, defined by the condition that
the expansion of the outgoing null normals vanishes ($\theta_+ = 0$).
Because it depends only on data on a single time slice, the apparent
horizon can be found during evolution, slice by slice. Under reasonable
energy conditions, the apparent horizon lies inside or coincides with
the event horizon (this is a theorem, not a numerical observation), so
it provides a practical proxy for the black hole boundary during
simulation.

In practice, apparent horizons are found far more frequently than event
horizons during numerical simulations. They provide real-time diagnostic
information: the horizon area gives the irreducible mass, the
angular momentum can be extracted from the horizon geometry, and
the approach of two apparent horizons toward a common apparent horizon
signals the onset of merger. Event horizons, found in postprocessing,
provide complementary information about global causal structure and
can reveal features invisible to the apparent horizon finder, including
temporary changes in horizon topology.

### 5.2 Early event horizon finders

Libson and collaborators [S24] and Massó and collaborators [S25] developed
the first systematic algorithms for locating event horizons in numerically
evolved spacetimes. The basic approach works backward in time. At late times,
when the black hole has settled to a nearly stationary state, the event
horizon is approximately known (it coincides with the apparent horizon for
stationary black holes). Null geodesics---the generators of the event
horizon---are then integrated backward in time from this late-time
surface into the dynamical regime.

The backward integration is more stable than forward integration because
the event horizon is an attractor in the backward time direction: nearby
null geodesics converge onto the horizon surface. In the forward direction,
nearby geodesics diverge exponentially, making the horizon a repeller and
forward integration impractical.

The second paper [S25] refined these methods and benchmarked them against
known analytic solutions (Kerr, Schwarzschild), establishing accuracy
criteria for production use. The emphasis on verification against known
solutions is characteristic of careful numerical work: one must demonstrate
that the algorithm reproduces known results before trusting it in regimes
where no analytic answer exists.

### 5.3 Thornburg's comprehensive review

Jonathan Thornburg's *Living Reviews in Relativity* article [S26] provides
exhaustive coverage of horizon-finding algorithms for 3+1 numerical
relativity. For event horizons, Thornburg analyzes three approaches in
order of increasing effectiveness:

Forward integration of null geodesics, which suffers from exponential
instability (the event horizon is an unstable surface in the forward time
direction). Backward integration of null geodesics, which is more stable
but can lose accuracy at caustics where generators cross. Backward
integration of null surfaces, which tracks the entire two-dimensional
surface rather than individual generators and achieves both efficiency and
accuracy.

For apparent horizons, the situation is algorithmically different. The
apparent horizon equation is an elliptic PDE on the two-sphere (or a
more general closed surface). Thornburg's own AHFinderDirect implementation
solves this equation using Newton's method with spectral angular
discretization, achieving rapid convergence for smooth horizons. The
review also discusses shooting methods (effective in axisymmetry but
difficult to generalize), Nakamura's algorithm, and various elliptic PDE
formulations.

The practical guidance on interpolation, initial guesses, and convergence
criteria makes this review valuable not only as a survey but as a
reference for implementation. If one is implementing a horizon finder for
a numerical relativity code, Thornburg's article is the natural starting
point.

### 5.4 Modern developments

Cohen, Pfeiffer, and Scheel [S27] revisited event horizon finding with
emphasis on computational efficiency and accuracy improvements. As binary
black hole simulations became routine following the 2005 breakthroughs,
the demands on horizon finders increased: long-duration simulations with
frequent horizon finding require fast algorithms, and the desire to resolve
fine features of horizon geometry (especially during merger) demands high
accuracy.

Bohn, Kidder, and Teukolsky [S28] developed a parallel adaptive event
horizon finder designed for production-scale three-dimensional simulations.
The algorithm dynamically adjusts the resolution of the triangulated
horizon surface based on local geometric features, concentrating
computational effort where the horizon curvature is largest. Parallelization
is essential: as numerical relativity simulations exploit thousands or
tens of thousands of processor cores, every component of the analysis
pipeline---including horizon finding---must parallelize efficiently.

### 5.5 Toroidal horizons

A companion paper by Bohn, Kidder, and Teukolsky [S29] investigates an
exotic feature of event horizons in binary black hole mergers: the
temporary formation of toroidal (doughnut-shaped) horizon topology. By
Hawking's topology theorem, cross-sections of the event horizon in a
stationary spacetime must have spherical topology. But during the
dynamical merger process, between the instant when the two separate
horizons merge into one and the moment when the merged horizon settles
into a topologically spherical configuration, the event horizon can
exhibit a brief toroidal phase.

This is not merely a mathematical curiosity. The existence of toroidal
horizon topology depends on the choice of spacetime foliation (the
slicing of spacetime into spatial hypersurfaces), which highlights a
conceptual subtlety: statements about horizon topology in dynamical
spacetimes require careful specification of how "space" and "time" are
defined. Resolving the brief toroidal phase numerically requires the
adaptive, high-resolution horizon-finding capabilities developed in [S28],
demonstrating the interplay between algorithmic development and physical
discovery.

The intellectual arc of the horizon-finding literature---from early
generator-based approaches [S24, S25] through comprehensive algorithmic
analysis [S26] to modern parallel-adaptive methods [S28] and their
application to exotic topology [S29]---is a microcosm of numerical
relativity's development. Each generation of algorithms was motivated
by physical questions that the preceding generation could not address,
and the improved algorithms in turn enabled discovery of new phenomena.


## 6. Gaps and Future Directions

These notes, in their present form, constitute an idiosyncratic sampling
rather than a comprehensive treatment. Several significant topics receive
limited or no coverage. The most relevant are: 

### 6.1 The breakthrough papers

The papers that transformed
numerical relativity in 2005--2006. Pretorius's generalized harmonic
simulation, Baker et al.'s and Campanelli et al.'s moving puncture
simulations --- represent the culmination of decades of
effort and the beginning of numerical relativity's transition from a
field struggling with stability to one producing routine, high-accuracy
results. 

### 6.2 Initial data construction

The constraint equations of general relativity (the Hamiltonian and
momentum constraints) must be satisfied by any initial data set before
evolution can begin. The conformal thin-sandwich approach, York's
conformal decomposition, and the spectral methods used to solve the
resulting elliptic equations are central to numerical relativity practice. 
Different solutions to the constraints
represent different physical configurations, and the relationship between
mathematical parameters in the initial data and physical quantities
(masses, spins, orbital parameters) requires careful analysis.

### 6.3 Gravitational wave extraction

The primary scientific output of most numerical relativity simulations is
the gravitational waveform---the time-dependent strain $h_+(t)$ and
$h_\times(t)$ that a distant gravitational wave detector would measure.
Extracting this waveform from the simulation requires either Newman--Penrose
formalism (computing the Weyl scalar $\Psi_4$ on coordinate spheres at
large radius) or Cauchy-characteristic extraction (matching the Cauchy
evolution to a characteristic evolution that propagates the waves to
future null infinity). Neither technique is represented in the current
bibliography. Given numerical relativity's central role in gravitational
wave astronomy---LIGO/Virgo template banks rely on numerical waveforms
for calibration and validation---this gap is notable

### 6.4 Formulation and gauge canon

The present bibliography cites the BSSN formulation implicitly through
the textbooks and toolkit papers but does not include the original
formulation papers (Shibata and Nakamura 1995; Baumgarte and Shapiro
1999) or the alternative formulations (generalized harmonic, Z4, CCZ4)
that play important roles in contemporary practice. Similarly, the
standard gauge conditions (1+log slicing, Gamma-driver shift) and the
theory of constraint damping lack dedicated references. For a reader
trying to understand *why* modern simulations work, these papers are
essential.

### 6.5 Relativistic hydrodynamics and magnetohydrodynamics

Binary neutron star mergers, core-collapse supernovae, and accretion
onto compact objects all require coupling Einstein's equations to matter
evolution. The finite-volume methods, equation-of-state microphysics,
and neutrino transport schemes used in these simulations constitute a
substantial subfield that the present notes do not address. Given the
multimessenger astronomy program---combining gravitational wave,
electromagnetic, and neutrino observations---this is an increasingly
important frontier.


## 7. Reading Paths

The references collected here, together with the two textbooks, support
several paths through the material depending on the reader's background
and goals.

For a reader learning numerical relativity from scratch, a viable
sequence would begin with a textbook-driven approach (Baumgarte--Shapiro
[S11] or Shibata [S15]) to establish the 3+1 decomposition, initial data
construction, and gauge conditions. The finite difference foundations
(Kreiss--Oliger [S4, S5]; higher-order schemes [S6]) and AMR theory
(Berger--Oliger [S8]; Berger--Colella [S9]) then provide the discretization
context. With this background, one can examine how these ideas are
implemented in the Einstein Toolkit [S12] or GRChombo [S13], and then
pursue one application track end-to-end.

For a reader interested specifically in critical phenomena, the path is
more focused: begin with the Gundlach--Martín-García review [S21] for
the theoretical framework, then read Choptuik's original paper [S19]
alongside the 2+1 extensions [S20, S22]. The Gregory--Laflamme endpoint
[S23] provides a connection to higher-dimensional gravity and cosmic
censorship.

For a reader implementing or understanding horizon finders, Thornburg's
review [S26] is the essential starting point, supplemented by the
event-horizon-specific papers [S24, S25, S27, S28] and the toroidal
topology investigation [S29].

For the broader view of what numerical relativity has discovered about
strong-field gravity, the reviews by Choptuik, Lehner, and Pretorius
[S14] and by Scheel and Thorne [S16] provide complementary perspectives,
the former emphasizing methodology and the latter physical discoveries.


## 8. Projects and Computational Exercises

The references collected here support several concrete computational
projects suitable for graduate students or researchers entering numerical
relativity. Each project connects foundational theory to hands-on
implementation.

### 8.1 Convergence testing and Richardson extrapolation

Implement a finite-difference solver for the one-dimensional wave equation
$\partial_t^2 u = c^2 \partial_x^2 u$ with second-order and fourth-order
spatial stencils. Verify convergence by running at three resolutions $h$,
$h/2$, $h/4$ and computing the Richardson extrapolation. Demonstrate
that the convergence order matches the theoretical prediction. Then add
Kreiss--Oliger dissipation and measure its effect on convergence order
and stability. This exercise makes concrete the techniques described in
Section 2 and provides direct experience with the verification methodology
used throughout numerical relativity.

### 8.2 AMR for a scalar wave equation

Using a publicly available AMR library (Chombo or AMReX), implement an
adaptive solver for the scalar wave equation in two or three spatial
dimensions with a localized initial pulse. The refinement criterion should
be based on a truncation error estimate following the Berger--Oliger
approach. Compare the computational cost (grid points $\times$ time steps)
of the AMR solution against a uniform grid solution at equivalent accuracy.
This project builds intuition for the multi-scale challenges that motivate
AMR in numerical relativity.

### 8.3 Scalar field collapse in spherical symmetry

The Einstein--scalar-field system in spherical symmetry provides an
accessible entry point to numerical relativity proper. The system reduces
to 1+1 dimensions, making it computationally tractable on modest hardware.
Implement the evolution equations (using either a null-coordinate or a
Cauchy formulation), evolve Gaussian initial data of varying amplitude,
and identify the threshold of black hole formation. With sufficient
numerical precision and resolution (AMR is recommended), attempt to
measure the Choptuik scaling exponent $\gamma$ and the echoing period
$\Delta$. This project connects the numerical methods of Section 2 to
the physics of Section 4 and is among the most rewarding exercises in
computational general relativity.

### 8.4 Apparent horizon finding

On a given time slice of a numerically evolved spacetime (data can be
generated from the Einstein Toolkit's standard test suite or downloaded
from the SXS collaboration's public waveform catalog), implement an
apparent horizon finder using the spectral method described by Thornburg
[S26]. The apparent horizon equation is an elliptic PDE on the two-sphere:
parameterize the horizon surface as $r = h(\theta, \phi)$, expand $h$ in
spherical harmonics, and solve the resulting nonlinear system using Newton's
method. Compare your results against the AHFinderDirect output included in
the Einstein Toolkit.

### 8.5 Einstein Toolkit walkthrough

Install the Einstein Toolkit and run one of the standard test cases: the
Brill wave test (a nonlinear gravitational wave in axisymmetry), the
Schwarzschild black hole in isotropic coordinates (testing gauge evolution
and constraint preservation), or the head-on collision of two black holes
(the simplest binary configuration). For each test case, monitor the
Hamiltonian constraint violation as a function of time and resolution,
and verify the expected convergence order. This project provides
first-hand experience with the community infrastructure described in
Section 3 and connects the theoretical material in Sections 2--3 to
practical simulation.


## Bibliography

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
