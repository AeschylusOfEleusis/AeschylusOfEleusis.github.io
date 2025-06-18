---
layout:   post
title: "Black holes"
date: 2025-06-08 10:00:00 +0800
categories: [Numerical Relativity]
tags: [Numerical Relativity, Quantum Field Theory, Black holes, Worm holes, Scientific Computing]
math:       true        # enable KaTeX
---
# Notes on Black holes (Draft)

## Abstract

Black holes, described by Chandrasekhar as "...*the simplest and most perfect objects in the universe...* ", are considered here with short notes. Sections include a sampling of the literature concerning: 1. The general theory of black holes, 2. Generic behavior of the black hole event horizon, 3. Scattering from black hole sources, and 4. Gravitational radiation from black hole collisions.   

**To be continued ...**

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
| S12  | [Poisson *“Advanced Course in General Relativity”* 2002](https://scholar.google.com/citations?view_op=view_citation&hl=en&user=xUg1urIAAAAJ&cstart=20&pagesize=80&sortby=pubdate&citation_for_view=xUg1urIAAAAJ:08ZZubdj9fEC) | Lecture notes covering null surfaces, including a detailed derivation of horizon boundary conditions.                     |
| S13  | [Gourghulon *“3+1 perspective on null surfaces”* 2005](https://arxiv.org/abs/gr-qc/0503113)                                                                     | Applies a 3+1 decomposition to characterize the geometry and evolution of null hypersurfaces such as event horizons.        |
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
