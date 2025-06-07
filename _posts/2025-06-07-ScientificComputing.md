---
layout:   post
title: "Scientific Computing"
date: 2025-06-07 10:00:00 +0800
categories: [Computational Finance]
tags: [Computational Finance, Numerical Relativity, Quantum Field Theory, Stochastic Calculus, PathIntegrals]
math:       true        # enable KaTeX
---
# Notes on Scientific Computing (Draft)

## Abstract
References in scientific computing are presented with short notes. Following an overview that includes general survey of applied mathematics, sections include numerical methods, engineering, and application domains.

### 1. Overview: Applied Mathematics and Scientific Computing

| ID  | Link                                                                                                                                                    | Notes                                                                            |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| S1  | [Roman “Advanced Linear Algebra” 2005](https://link.springer.com/book/10.1007/978-0-387-72831-5)                                                        | Provides a rigorous treatment of vector spaces, modules, and canonical forms.    |
| S2  | [Landau et al “First Course Scientific Computing” 2005](https://www.jstor.org/stable/j.ctvcm4grd)                                                      | Introduces fundamental algorithms and practical techniques for scientific computing. |
| S3  | [Press et al “Numerical Recipes” 2007](https://numerical.recipes/book.html)                                                                            | Presents a collection of tested numerical algorithms with code examples.         |
| S4  | [Strang “Computational Science” 2007](https://math.mit.edu/~gs/cse/)                                                                                  | Surveys computational methods and applications taught in an MIT engineering course. |
| S5  | [Higham “Princeton Companion Applied Mathematics”](https://press.princeton.edu/books/hardcover/9780691150390/the-princeton-companion-to-applied-mathematics?srsltid=AfmBOor_w1EnIjOrPW3sPT621YIeddTNBR1W1Gzs5TNXVt02nDJri1lB) | Offers expert essays on foundational and emerging topics in applied mathematics. |
| S6  | [Strang “Linear Algebra” 2016](https://math.mit.edu/~gs/linearalgebra/ila5/indexila5.html)                                                             | Modern textbook emphasizing computational aspects of linear algebra.            |
| S7  | [Galassi et al “Gnu Scientific Library” 2021](https://www.gnu.org/software/gsl/)                                                                       | Documentation and guide to a comprehensive C/C++ library for numerical computing. |

---
### 2. Methods: Numerical Analysis

| ID   | Link                                                                                                                                               | Notes                                                                                          |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| S8   | [Lanczos “Applied Analysis” 1952](https://store.doverpublications.com/products/9780486656564?srsltid=AfmBOoozet4k21Mdbo919f3Rz37Y3CDGIUygNNSZO72V5-u-IMSfbc4p)   | Classic text on functional analysis methods applied to differential equations.                |
| S9   | [Stoer and Burlisch “Numerical Analysis” 1980](https://link.springer.com/book/10.1007/978-1-4757-5592-3)                                           | Authoritative treatment of numerical algorithms and error estimation.                          |
| S10  | [Ridgway and Scott “Numerical Analysis” 2011](https://press.princeton.edu/books/hardcover/9780691146867/numerical-analysis?srsltid=AfmBOorDTHcEfIknS7PEjgoC1QPhVbIAZjiNYMdBgFHxr9O6_eZDVhJl) | Contemporary introduction to core numerical methods with practical examples and theory.       |

---

### 3. Methods: Monte Carlo

| ID   | Link                                                                                                                                                       | Notes                                                                                           |
|------|------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| S11  | [Metropolis and Ulam “Monte Carlo” 1949](https://www.tandfonline.com/doi/abs/10.1080/01621459.1949.10483310)                                               | Foundational paper introducing stochastic simulation for statistical physics.                   |
| S12  | [Rubinstein and Kroese “Simulation and Monte Carlo” 2017](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118631980)                                   | Comprehensive guide to Monte Carlo methods and variance-reduction techniques.                   |
| S13  | [Cheng et al “Langevin MCMC on Reimannian Manifolds” 2024](https://arxiv.org/abs/2402.10357)                                                              | Proposes manifold-based Langevin algorithms to enhance sampling efficiency.                     |

---
### 4. Engineering

| ID   | Link                                                                                                                                                            | Notes                                                                                           |
|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| S14  | [Stroustrup “C++” 1997](https://www.stroustrup.com/4th.html)                                                                                                     | Definitive reference for the design and use of the C++ programming language.                    |
| S15  | [Viswanath “Scientific Programming and Architecture” 2007](https://mitpress.mit.edu/9780262036290/scientific-programming-and-computer-architecture/)              | Explores the interplay between software design and computer architecture in scientific computing. |
| S16  | [Arpaci-Dusseau “Operating Systems” 2018](https://pages.cs.wisc.edu/~remzi/OSTEP/)                                                                              | Comprehensive introduction to modern OS concepts and implementations.                            |
| S17  | [Hein et al “Unix Administration Handbook” 2018](https://www.oreilly.com/library/view/unix-and-linux/9780134278308/)                                             | Practical guide to Unix/Linux system administration best practices.                              |
| S18  | [Eijkhout “The Art of HPC Vol 1 - Vol 4” 2022](https://theartofhpc.com)                                                                                          | Multi-volume series on high-performance computing and parallel programming techniques.           |
| S19  | [Washizaki “SwE Body of Knowledge v4.0” 2024](https://www.computer.org/education/bodies-of-knowledge/software-engineering)                                        | Authoritative framework detailing core knowledge areas in software engineering.                 |
| S20  | [Hennessy et al “Computer Architecture” 2025](https://shop.elsevier.com/books/computer-architecture/hennessy/978-0-443-15406-5)                                    | Up-to-date textbook on the principles and practice of computer architecture.                     |

---

### 5. Applications: Modeling

| ID   | Link                                                                                                                                                                    | Notes                                                                                          |
|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| S21  | [Peskin “Flow around a heart valve: Numerical Method” 1972](https://www.sciencedirect.com/science/article/abs/pii/0021999172900654)                                      | Introduces a finite-difference method for simulating blood flow around heart valves.           |
| S22  | [Peskin “Immersed Boundary Method” 2002](https://www.cambridge.org/core/journals/acta-numerica/article/immersed-boundary-method/95ECDAC5D1824285563270D6DD70DA9A#)           | Presents the immersed boundary method for fluid–structure interaction problems.                |
| S23  | [Toyer “Computational Neuroscience” 2005](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=4d50c75a9f01decfa498d3f331121f988e21ee51)                         | Surveys mathematical and computational models of neural systems.                               |
| S24  | [Kellis “Computational Biology” 2016](https://compbio.mit.edu/teaching/book.pdf)                                                                                         | Textbook on algorithms and models for computational analysis in biology and genomics.          |
| S25  | [Boudreau and Swanson “Applied Computational Physics” 2018](https://global.oup.com/academic/product/applied-computational-physics-9780198708636?cc=us&lang=en&)             | Explores computational techniques applied to diverse physics problems with case studies.       |

---


### 6. Applications: Data

| ID   | Link                                                                                                                                                                 | Notes                                                                                      |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| S26  | [Bohm and Zech “Introduction to Statistics and Data” 2010](https://www-library.desy.de/preparch/books/vstatmp_engl.pdf)                                               | Provides a foundational overview of statistical methods and data analysis techniques.     |
| S27  | [Singer and Wu “Vector Diffusion Maps” 2012](https://web.math.princeton.edu/~amits/publications/VDMrevision_final.pdf)                                               | Introduces vector diffusion maps for manifold-structured data dimensionality reduction.   |
| S28  | [Leskovec et al “Massive Data”](https://www.cambridge.org/core/books/mining-of-massive-datasets/A06D57FC616AE3FD10007D89E73F8B92#fndtn-information)                                                                                   | Comprehensive discussion of algorithms for mining and analyzing large-scale networks.     |
| S29  | [Das “Data Science” 2017](https://srdas.github.io/MLBook/)                                                                                                            | Practical guide to data science methodologies and machine learning workflows.             |
| S30  | [Kremer et al “Data in Astronomy” 207](https://arxiv.org/abs/1704.04650)                                                                                              | Examines big-data challenges and solutions in astronomical data analysis.                 |
| S31  | [Nature Physics “The Thing About Data” 2017](https://www.nature.com/articles/nphys4238)                                                                               | Editorial on the impact and challenges of data-driven research in physics.                |
| S32  | [Blum et al “Foundations of Data” 2018](https://www.cs.cornell.edu/jeh/book.pdf)                                                                                     | Comprehensive treatment of data structures and algorithms foundational to data science.   |
| S33  | [McNicholas and Tair “Data Science with Julia” 2019](https://www.taylorfrancis.com/books/mono/10.1201/9781351013673/data-science-julia-peter-tait-paul-mcnicholas)          | Guide to implementing data science workflows using the Julia programming language.        |
| S34  | [James et al “Introduction Statistical Learning” 2023](https://www.statlearning.com)                                                                                  | Modern introduction to statistical learning techniques with applied R examples.           |
| S35  | [Sethna “Sloppy Models” 2024](https://sethna.lassp.cornell.edu/Teaching/BasicTraining/SloppyBook.pdf)                                                                 | Analyzes parameter sensitivity and robustness in complex scientific models.               |