---
layout:   post
title: "Machine Learning"
date: 2025-05-31 10:00:00 +0800
categories: [Computational Finance]
tags: [Machine Learning, Probability Information Risk, Numerical Relativity, Quantum Field Theory, Computational Finance]
math:       true        # enable KaTeX
---
# Notes on Machine Learning (Draft)

## Abstract

These notes provide an annotated guide to the literature on machine learning, organized around the probabilistic view of inference and learning. The treatment is intended for students and practitioners with training in physics or applied mathematics who wish to understand machine learning not merely as an engineering discipline but as a subject with deep structural connections to statistical mechanics, field theory, and stochastic dynamics. Applications and illustrations are drawn predominantly from theoretical physics, numerical relativity, and quantum field theory. The notes are organized into fourteen sections that mirror the logical structure of the subject, progressing from probabilistic foundations through neural architectures and generative models to sequence learning and decision-making. Five canonical textbooks form the stable backbone; sixty-four supplementary references constitute the research frontier. The result is an idiosyncratic guide to a literature that, at its best, reveals machine learning and statistical physics to be two dialects of the same mathematical language.

---

## Introduction

Machine learning, viewed from the perspective of a physicist, is the study of inference in high-dimensional probability distributions. The dominant narrative in the field emphasizes software engineering, benchmark performance, and scaling laws. That narrative is not wrong, but it is incomplete. There exists a parallel intellectual tradition---less visible in the machine learning conferences, more visible in *Physical Review* and *Journal of Statistical Physics*---that asks structural questions about why neural networks work, what determines their generalization, and how the mathematical tools of statistical field theory illuminate the geometry of learning.

These notes are written from within that second tradition. The organizing principle is probabilistic: learning is inference, architectures encode priors, training is dynamics, and generalization is controlled by the effective dimensionality of the learned representation. The applications are drawn from physics---gravitational wave detection, surrogate modeling of the Einstein equations, PDE solvers, and the emerging neural network--quantum field theory (NN--QFT) correspondence---not because physics is the only domain where machine learning matters, but because these applications make the mathematical structure most transparent.

The notes are structured around five textbooks that collectively span the field: Bishop's *Pattern Recognition and Machine Learning* (2006) and *Deep Learning: Foundations and Concepts* (2024), Goodfellow, Bengio, and Courville's *Deep Learning* (2016), and Murphy's two-volume *Probabilistic Machine Learning* (2022, 2023). These serve as the stable backbone. Sixty-four supplementary references (labeled S1 through S64) constitute the volatile frontier---the research papers, monographs, and lecture notes where the most interesting ideas live. The textbooks teach the standard material; the supplementary readings reveal its hidden connections to physics.

A word on intended audience. These notes assume familiarity with probability theory at the level of a first graduate course, linear algebra, and the basics of differential equations. Some facility with statistical mechanics (partition functions, free energies, mean-field theory) will make certain sections more natural, but is not strictly required---the notes develop the relevant physical intuition as it arises. Conversely, readers approaching from the physics side will find that the textbook references supply whatever ML-specific vocabulary they lack.

The sections are ordered to reflect both logical dependence and increasing conceptual depth. Sections 1--4 establish foundations: the probabilistic framework, linear models, and classification. Sections 5--7 introduce neural networks, kernel methods, and regularization---the core toolkit. Section 8 marks a turning point: graphical models serve as the gateway to field-theoretic methods and the NN--QFT correspondence, which is the theoretical centerpiece of these notes. Sections 9--12 develop generative models, approximate inference, and sampling---the stochastic dynamics that connect machine learning to Langevin equations and path integrals. Section 13 applies these ideas to sequence and time-series problems, with gravitational wave science as a capstone domain. Section 14 closes with decision-making, causality, and frontier topics.

A recommended path through the material: begin with Sections 1--2 for orientation, proceed through 3--5 for the core ML toolkit, then take up Sections 6--8 where the physics connections become explicit. Sections 9--12 can be read in any order depending on interest, though 10 (generative models) benefits from 9 (latent variables). Section 13 is largely self-contained for readers interested in the gravitational wave applications. Section 14 is intentionally compact and points toward open research directions.


## The Textbook Spine

The five textbooks anchoring these notes were chosen to provide complementary perspectives on a common body of material. Understanding what each contributes clarifies the role of the supplementary readings.

**Bishop (2006), *Pattern Recognition and Machine Learning* (PRML-06).** The classic probabilistic treatment. Its graphical models chapters (8--10) and appendices on distributions and matrix identities remain indispensable reference material two decades after publication. Where these notes cite PRML-06, it is typically for its treatment of directed and undirected graphical models, belief propagation, and the EM algorithm.

**Goodfellow, Bengio, and Courville (2016), *Deep Learning*.** The engineering-side reference. Its strength is the systematic treatment of deep feedforward networks, convolutional architectures, regularization strategies, and optimization algorithms. It was written before the diffusion model revolution and the transformer's dominance, so it provides an excellent foundation that the supplementary readings update.

**Murphy (2022), *Probabilistic Machine Learning: An Introduction*.** The modern Bayesian treatment of introductory material. Stronger than Goodfellow on probability, priors, and decision theory; particularly useful for its coverage of GLMs, kernel methods, and ensemble learning from a probabilistic viewpoint.

**Murphy (2023), *Probabilistic Machine Learning: Advanced Topics*.** The most comprehensive single-volume treatment of modern probabilistic ML. Covers variational inference, Gaussian processes, normalizing flows, diffusion models, energy-based models, and causal inference. Where Goodfellow provides the 2016 engineering perspective, Murphy (2023) provides the 2023 probabilistic perspective.

**Bishop (2024), *Deep Learning: Foundations and Concepts*.** A thorough update incorporating the developments of the past decade: transformers, diffusion models, double descent, modern regularization. Serves as a conceptual bridge between the classic probabilistic treatment of PRML-06 and the engineering perspective of Goodfellow.

The supplementary references (S1--S64) are keyed to these textbooks: each section begins with the relevant textbook chapters and then presents the research literature that extends, applies, or reinterprets the textbook material through a physics lens. The textbooks provide the standard curriculum; the supplementary readings provide the intellectual argument that animates these notes.


## 1. Overview

The first section orients the reader by establishing the dual perspective that runs through all fourteen sections: machine learning can be understood through physics, and physics benefits from machine learning methods. The textbook anchors lay the conventional groundwork. Bishop-24 Chapter 1 provides a historical tour from perceptrons to modern deep learning. Goodfellow-16 Chapter 1 frames deep learning as the "third wave" of AI, following symbolic methods and classical statistical learning, with representation learning as the distinguishing innovation. Murphy-22 Chapters 1 and 5 establish the Bayesian decision-theoretic framework---learning as rational decision-making under uncertainty---that provides the probabilistic spine for everything that follows. Murphy-23 Chapter 1 surveys the advanced landscape.

The supplementary readings for this section signal the bibliography's intended audience. Ganguli and collaborators (S1, arXiv 1301.7115) review statistical mechanics applied to neural systems and high-dimensional data, introducing replica theory for analyzing learning in random networks and connecting message passing in graphical models to neural computation. This is not a deep learning history paper; it is a statistical mechanics paper that happens to concern neural networks, and the distinction matters for understanding how these notes approach the subject.

Mehta et al. (S2, arXiv 1803.08823) provide the primary bridge text: a 122-page pedagogical review published in *Physics Reports*, complete with Jupyter notebooks using physics datasets (Ising model configurations, Monte Carlo simulations). The paper emphasizes the natural connections between ML and statistical physics---energy-based models, variational methods, the replica trick---and is the single best entry point for a physicist approaching machine learning for the first time.

The remaining overview sources range from surveys of ML in the physical sciences (Carleo et al., S4, Nature Reviews Physics; S7, Nature Physics) through monographs on quantum physics and deep learning (S5, Springer 2020) to more speculative programmatic essays. Roberts (S9, arXiv 2104.00008) argues that the effectiveness of deep learning, like Wigner's "unreasonable effectiveness of mathematics," reflects the sparsity principle: both physics and ML exploit the fact that most possible functions are not realized in nature. The TASI lectures (S11, arXiv 2408.00082) provide a graduate-student gateway to the physics--ML interface.

Collectively, these sources establish that the bibliography is not a general ML reading list. It is a physics-facing reading list that takes ML seriously as a mathematical subject. Readers expecting coverage of data pipelines, scaling recipes, or benchmark culture will not find it here. What they will find is a coherent intellectual program: the claim that the tools of statistical field theory illuminate why machine learning works, not merely how to make it work.


## 2. Probability and Statistical Foundations

The probabilistic framework is the foundation on which everything else rests. The textbook coverage is comprehensive: Bishop-24 Chapters 2--3 develop Bayesian inference, KL-divergence, and a catalogue of standard distributions. Goodfellow-16 Chapters 2--4 supply the linear algebra, probability, and information theory prerequisites. Murphy-22 Chapters 2--4 and 6 provide deeper probabilistic modeling with emphasis on conjugate priors. Murphy-23 Chapters 2--3 and 5 introduce information geometry (the Fisher information metric, natural gradients) and exponential families. PRML-06 Appendices B--C serve as lookup references for distribution properties and matrix identities.

The supplementary readings for this section set up the field-theoretic perspective that distinguishes these notes from standard ML treatments. Bialek, Callan, and Strong (S22, arXiv cond-mat/9607180) is a seminal paper that demonstrates a fact of considerable importance: Bayesian priors over probability distributions define scalar field theories. In one dimension, the free field theory with a normalization constraint provides a tractable formulation. The central insight is that learning about distributions is equivalent to inference in a field theory, where the prior is the action and conditioning on data corresponds to adding source terms. This paper establishes the mathematical foundation for the NN--QFT correspondence that appears in Section 8.

The sequel (S23, arXiv cond-mat/0009165) extends the field-theoretic formulation to time-varying data, introducing path-integral representations for sequential learning. This connects to the stochastic process theory developed later in Sections 10--12 and to the temporal models of Section 13.

The remaining references illustrate different facets of the probabilistic program. S24 (PubMed 25018724) demonstrates Bayesian model averaging in neuroscience. S26 (arXiv 2112.01388) shows that theoretically motivated priors maintain their benefits even under the engineering approximations required for practical deep learning---a reassuring result for those who worry that Bayesian principles are too fragile for real systems. S27 (arXiv 2305.10491) connects renormalization to Bayesian evidence computation, showing that model comparison via Bayes factors can be computed through RG-like coarse-graining procedures. This last connection is conceptually important: it suggests that model selection and dimensionality reduction are manifestations of the same underlying principle.

The key takeaway from this section is that probability theory and field theory are not merely analogous but formally equivalent when the object of inference is a probability distribution. The prior over distributions is the action; the normalization constraint corresponds to a gauge-like symmetry; learning corresponds to conditioning, which in field-theoretic terms is computing Green functions with sources. This is not a metaphor. It is a mathematical identity that the subsequent sections exploit.


## 3. Linear Regression and Generalised Linear Models

Linear models serve as the exactly solvable limit of machine learning. Just as free field theories in physics admit closed-form solutions for all correlation functions via Wick's theorem, linear regression admits closed-form solutions for parameter estimates and predictive distributions. The value of studying them is not that they are practically important (though they are), but that they provide the baseline against which more complex models are understood.

Bishop-24 Chapter 4 frames ordinary least squares as a single-layer network with squared loss, deriving the Bayesian interpretation of regularization: L2 (Ridge) corresponds to a Gaussian prior on weights; L1 (LASSO) corresponds to a Laplace prior favoring sparsity. Murphy-22 Chapters 8 and 12 develop the full GLM framework---logistic regression for binary outcomes, Poisson regression for count data, and the general exponential-family formulation. Murphy-23 Chapter 15 provides the asymptotic statistical treatment, connecting to information geometry through the Fisher information.

The single supplementary reference for this section (S12, arXiv 1702.01522) is a concrete example of the physics--ML bidirectionality that characterizes these notes. The paper converts the inverse Ising problem---inferring coupling constants from observed spin configurations---into penalized linear regression. L1 regularization (LASSO) corresponds to assuming sparse couplings; L2 regularization (Ridge) corresponds to assuming couplings are small but dense. The pseudolikelihood approximation converts the intractable partition function problem into tractable logistic regression.

This is worth pausing on. The inverse Ising problem is a statistical physics problem that was considered difficult because of the partition function. Reformulating it as penalized regression makes it a standard machine learning problem solvable with off-the-shelf convex optimization. Conversely, the physics perspective reveals that regularization---which in ML is motivated by the bias-variance tradeoff---has a physical interpretation as a prior on coupling structure. The linearity is in the regression, not in the underlying physics.

In field-theoretic language, the GLM framework corresponds to different free field theories with various propagators. The Gaussian likelihood gives the standard scalar propagator; the Bernoulli/logistic gives a discretized version; the Poisson gives a rate model. Each is an exactly solvable starting point for perturbative analysis.


## 4. Linear Classification

Bishop-24 Chapter 5 develops logistic-sigmoid networks and softmax regression for multi-class classification. Murphy-22 Chapters 9--10 present Fisher linear discriminant analysis, quadratic discriminant analysis, and the logistic regression foundations, contrasting generative approaches (modeling class-conditional densities) with discriminative approaches (modeling the decision boundary directly).

No supplementary sources are listed for this section, and this is intentional. Linear classification serves primarily as a bridge between the exactly solvable models of Section 3 and the neural networks of Section 5. The sigmoid and softmax functions that appear here become the prototypical nonlinearities in deeper architectures. From a field-theoretic perspective, the sigmoid introduces the simplest form of interaction---a nonlinearity that couples different modes and prevents exact analytical solution. The absence of physics-facing supplementary readings reflects the fact that linear classification does not naturally connect to field theory; it requires the nonlinear extensions of subsequent sections to make the correspondence precise.

Readers primarily interested in the physics connections may proceed quickly to Section 5, returning here only as needed for vocabulary (discriminant functions, decision boundaries, the generative-discriminative distinction).


## 5. Neural Networks and Deep Learning

This section is the practical core of the bibliography, where the neural network--physics connection becomes concrete. The textbook coverage is substantial. Bishop-24 treats multilayer perceptrons and backpropagation (Chapter 6), regularization including dropout and batch normalization (Chapter 8), and convolutional architectures (Chapter 10). Goodfellow-16 Chapters 6--9 provide the engineering-side treatment. Murphy-22 Chapters 11--13 cover the same architectures from a probabilistic perspective, emphasizing the correspondence between network outputs and predictive distributions. Murphy-23 Chapters 16--17 address very deep architectures (ResNets, DenseNets) and Bayesian neural networks, including the neural tangent kernel theory and infinite-width limits that connect directly to the field-theoretic perspective.

The supplementary readings organize into three coherent clusters.

**Symmetry-aware architectures.** The geometric deep learning trilogy (S28--S30) establishes that symmetry should be built into architectures rather than learned from data. S28 (arXiv 1906.02481) elevates CNNs from translation-equivariant to general equivariant spaces, showing that the translation equivariance of standard CNNs generalizes to arbitrary groups. S29 (arXiv 2002.12880) extends this to continuous Lie-group symmetries. S30 (arXiv 2104.13478) provides the comprehensive geometric deep learning roadmap, connecting CNNs, graph neural networks, and transformers through the unifying principle that symmetries constrain the space of useful architectures. This is the ML analogue of Noether's theorem: conservation laws follow from symmetries, and architectures that respect symmetries need not waste capacity learning them.

**Physics-informed architectures.** Hamiltonian neural networks (S31, arXiv 1906.01563) conserve energy by construction through symplectic integration. Extensions address higher-order Lagrangian systems (S32, arXiv 2010.13581), Lagrangian dynamics via the Euler--Lagrange equations directly (S33, arXiv 2003.04630), and constraint handling via Lagrange multipliers for robotics and molecular simulation (S34, arXiv 2202.04836). The reviews (S35, Nature Reviews Physics 2021; S36, arXiv 2203.16797) survey the physics-informed ML field comprehensively. S37 (arXiv 2304.14994) covers U-Net surrogates for PDE solvers, demonstrating speedups of two to three orders of magnitude over traditional numerical methods.

**Wide-network theory.** Two papers establish the analytical foundations for the NN--QFT correspondence. S41 (Physical Review E 98) applies path-integral methods to wide-network learning trajectories, showing that the loss landscape corresponds to an effective potential and gradient descent corresponds to relaxation dynamics. S43 (arXiv 1910.00019) develops neural tangent kernel (NTK) theory, proving that infinite-width networks evolve as linear models under gradient descent in the "lazy training" regime. This corresponds to the Gaussian process / free field theory limit, providing exact analytical control over network behavior.

The structure of the supplementary readings reveals a coherent program: geometry and symmetry constrain what architectures are useful (S28--S30); physics priors make architectures sample-efficient and physically consistent (S31--S37); and the infinite-width limit admits exact analysis via Gaussian processes and path integrals (S41, S43), providing the bridge to field theory in Section 8.


## 6. Kernel Methods and Gaussian Processes

Murphy-22 Chapter 17 covers SVMs, the kernel trick, and kernel ridge regression. Murphy-23 Chapter 18 provides the full Bayesian treatment of Gaussian processes, including variational and sparse approximations for scaling.

Gaussian processes are the free field theory of machine learning. They are exactly solvable models where all correlation functions factor into products of the kernel (the two-point function), exactly as free field theory correlation functions factor via Wick's theorem. The connection between infinite-width neural networks and GPs, established rigorously by NTK theory (S43 in Section 5), means that GP theory provides exact predictions for wide networks: the NNGP (neural network Gaussian process) and NTK correspondences show that wide neural networks *are* GPs, with specific kernel functions determined by the architecture and activation.

The single supplementary reference (S19, RMT4ML notes 2023) introduces random matrix theory (RMT) for diagnosing kernel learning in high dimensions. RMT provides exact results for the eigenvalue spectrum of kernel matrices in the proportional scaling limit (both the number of features and the number of samples growing, with their ratio held fixed). The Marchenko--Pastur distribution describes the bulk eigenvalue spectrum; Tracy--Widom statistics govern the edge. The practical consequence is precise characterization of when kernels overfit (bulk eigenvalues extending to zero), when they generalize (separated spike eigenvalues capturing signal), and the spectral signatures of each regime.

This section is lean by design. Its role is to establish the free-theory baseline---the exactly solvable limit---against which the interacting theories of Sections 7 and 8 are measured. The GP/NTK correspondence means that understanding GPs is prerequisite to understanding the perturbative corrections that finite-width networks introduce.


## 7. Regularisation and Ensemble Learning

Regularization has a physical interpretation that is both precise and illuminating: it corresponds to modifying the action of the field theory to improve its statistical properties.

Goodfellow-16 Chapter 7 covers the practical toolkit: dropout, L1/L2 regularization, data augmentation, early stopping, noise injection. Bishop-24 Chapter 9 provides the modern perspective including batch normalization, residual paths, double descent, and pruning. Murphy-22 Chapters 16 and 18 cover kNN, sparsity methods, tree ensembles, and boosting.

The supplementary readings develop the statistical physics interpretation. S13 (Ganguli group, StatMechDeep) provides a free-energy landscape view: L2 regularization corresponds to adding a mass term in field theory, preventing the field from fluctuating too wildly; dropout corresponds to disorder averaging, connecting to spin glass physics. S14 (Physica A 2023) studies how different penalty terms sculpt loss surfaces, creating qualitatively different landscape geometries that affect both optimization dynamics and generalization properties. S18 (arXiv 2306.02108) applies random matrix theory to loss surface Hessians, providing exact characterization of eigenvalue distributions at critical points. The main finding is that most critical points in high dimensions are saddle points, not local minima, and gradient descent can escape them. This resolves an old worry: the high-dimensional loss landscape is not the pathological wasteland that naive intuition (from low-dimensional visualization) suggests.

S56 (arXiv 1709.02470) addresses double descent---the phenomenon where test error decreases, then increases, then decreases again as model complexity grows past the interpolation threshold. This is completely invisible to classical bias-variance analysis but natural in the statistical physics framework: there is a phase boundary at the interpolation threshold, and behavior is qualitatively different on either side. The double-descent curve has been observed in kernel regression, random features models, and neural networks, and its explanation through the replica method and RMT represents a vindication of the statistical physics perspective. A caveat: the universality of double descent across architectures and datasets is not established. It appears clearly in specific solvable models but should not be taken as a universal law without qualification.

The physical dictionary is worth stating explicitly. L2 regularization corresponds to a mass term. L1 regularization corresponds to a non-analytic potential favoring sparsity. Dropout corresponds to quenched disorder. Early stopping corresponds to a finite-time cutoff in the relaxation dynamics. Temperature (in the statistical mechanics sense) maps to learning rate. These identifications follow from the mathematical correspondence between the loss function and the energy in a statistical mechanical system.


## 8. Graphical Models and Structured Probability

This section marks the conceptual turning point of the notes. The textbook anchors are classical---Bishop-24 Chapter 11 on factor graphs, HMMs, and autoregressive densities; Murphy-23 Chapters 4 and 30 on structure learning and graph inference; PRML-06 Chapters 8--10 on directed and undirected graphical models. But the supplementary readings take a sharp turn from mainstream PGM practice toward field theory.

The section title is "Graphical Models and Structured Probability," but what it actually develops is the neural network--quantum field theory correspondence. The connection is not arbitrary: energy-based models and Markov random fields are the classical bridge between graphical models and statistical mechanics. The Hammersley--Clifford theorem tells us that a positive distribution factorizing over the cliques of an undirected graph is a Gibbs distribution---equivalently, a lattice field theory. This is the mathematical door through which field theory enters machine learning.

**The statistical field theory of neural networks.** Helias and Dahmen (S42, arXiv 1901.10416; S44, Springer 2020) provide a comprehensive treatment of generating functionals, cumulants, Wick's theorem, and diagrammatic perturbation theory for neural systems. They introduce the MSRDJ (Martin--Siggia--Rose--Janssen--de Dominicis) path integral formalism for stochastic neural dynamics and derive Thouless--Anderson--Palmer mean-field equations. The monograph (S44) is the most thorough single reference bridging field theory and neural networks.

**The NN--QFT correspondence.** Grosvenor and Jefferson (S45, arXiv 2109.13247) review the deep learning--QFT correspondence, presenting mean-field theory as a saddle-point approximation with loop corrections controlled by the ratio of depth to width. The critical point for information propagation---the "edge of chaos"---corresponds to tuning to a phase transition. Roberts, Yaida, and Hanin (S46, arXiv 2106.10165; Cambridge University Press) develop an effective theory approach showing that networks are nearly-Gaussian with controlled deviations, identifying universality classes for different activation functions. Halverson et al. (S47, arXiv 2008.08601) establish the foundational correspondence: the infinite-width limit maps to free field theory, finite-width corrections map to interactions, and Feynman diagrams provide a computational tool for evaluating these corrections.

**The reverse direction.** Bachtis et al. (S48, arXiv 2102.09449) work from QFT toward ML, showing that lattice scalar field theory satisfies the Hammersley--Clifford conditions and thus defines a Markov random field. This makes the correspondence bidirectional: not only can neural networks be analyzed as field theories, but lattice field theories can be implemented as specific neural network architectures.

**Stochastic dynamics and the MSRDJ formalism.** Helias et al. (S49, arXiv 1812.09345) connect the Onsager--Machlup and MSRDJ formalisms for stochastic neural dynamics. The two formulations are related by a Legendre transformation, exactly as in the relationship between the Lagrangian and Hamiltonian formulations of classical mechanics. This is directly relevant to stochastic quantization research, where the MSRDJ action provides the path-integral formulation for Langevin dynamics.

**Nonperturbative renormalization.** Erbin, Lahoche, and Samary (S50, arXiv 2212.11811; S51, arXiv 2108.01403) implement the Wetterich--Morris exact renormalization group equation for neural networks. The weight distribution variance acts as the RG flow parameter, and the flow equation describes how the effective action evolves as one integrates out degrees of freedom. This is the nonperturbative complement to the perturbative (Feynman diagram) approach of S47.

The NN--QFT correspondence, as documented in these sources, can be summarized in schematic form. Statistical ensembles of neural networks map to Euclidean quantum field theories. The infinite-width limit corresponds to free field theory (Gaussian processes). Finite-width corrections correspond to interactions (non-Gaussianity). The variance of weight initialization plays the role of a coupling constant. Criticality conditions (the "edge of chaos") correspond to tuning to a phase transition. Training dynamics, at least in certain regimes, can be described as flows in theory space.

Several caveats are essential. The claim that "training corresponds to RG flow" is best understood as a programmatic hypothesis that takes different precise forms in different papers; different authors mean different things by "RG" in this context (signal propagation RG, parameter flow, coarse-graining). The correspondence is most precisely established in the infinite-width and near-Gaussian limits; the strongly-coupled regime (narrow networks) remains challenging, just as strongly-coupled QFTs are. The identification of width with the inverse of a coupling constant is a useful organizing analogy in the large-$N$ expansion, but it should be presented as an interpretation rather than as a settled identification across all the cited works. These are active research questions, and the reader should approach the more expansive claims in the literature with appropriate calibration.

What is not in doubt is that the mathematical tools---generating functionals, perturbation theory, the RG equation, mean-field theory---provide calculational access to properties of neural network ensembles that are otherwise inaccessible. Whether this constitutes a "correspondence" in the strong sense of theoretical physics, or a productive mathematical framework, is a question the field is still settling.


## 9. Dimensionality Reduction and Latent Variables

Bishop-24 Chapters 16 and 19 progress from PCA, probabilistic PCA, factor analysis, and ICA to variational autoencoders and deep latent variable models. Goodfellow-16 Chapters 13--14 cover linear factor models and autoencoders. Murphy-22 Chapter 20 addresses nonlinear manifold learning (t-SNE, UMAP, Isomap, kernel PCA). Murphy-23 Chapters 27--28 and 32 cover representation learning, contrastive learning, and self-supervised methods.

The two supplementary references develop a renormalization group interpretation of dimensionality reduction. S54 (arXiv 1610.09733) connects PCA eigenvalue spectra to RG flows: the eigenvalue spectrum of the data covariance matrix reveals scale structure. Large eigenvalues correspond to relevant operators (in the RG sense) that survive coarse-graining; small eigenvalues correspond to irrelevant operators that can be safely truncated. Dimensionality reduction, in this view, is coarse-graining: keeping the relevant degrees of freedom and integrating out the irrelevant ones, exactly as in the construction of effective field theories.

S55 (Journal of Statistical Physics 2017) extends this analysis to biological and financial data, demonstrating that the spectral structure revealing "relevant" dimensions is not specific to physics datasets but appears in complex systems generally. This is a hint of universality---the same mathematical framework applies across domains---and it provides principled justification for dimension reduction beyond the standard appeal to the variance explained.

The RG interpretation connects directly to the NN--QFT correspondence: learning representations is learning which operators are relevant under the RG flow induced by the data distribution. Autoencoders, VAEs, and other representation learning methods are learned implementations of this principle, finding nonlinear transformations that extract the relevant degrees of freedom. The information bottleneck principle---keeping what is predictive and discarding what is not---is the information-theoretic shadow of RG relevance.


## 10. Deep Generative Models

This section is where stochastic calculus meets deep learning most directly. The textbook coverage is comprehensive: Bishop-24 treats discrete latent models, GANs, normalizing flows, and diffusion models across Chapters 15, 17, 18, and 20. Goodfellow-16 Chapter 20 provides the pre-diffusion survey. Murphy-23 Chapters 20--26 offer the most thorough textbook treatment of modern generative models from a probabilistic perspective.

The supplementary readings are organized around the stochastic dynamics of generation. S3 (tutorial PDF) provides a practical introduction to VAEs and denoising autoencoders. The conceptually important papers are those that establish the connection between generative modeling and stochastic differential equations.

Ho et al. (S20, arXiv 2006.11239) introduced denoising diffusion probabilistic models (DDPMs), establishing the connection between score matching (learning the gradient of the log-density), denoising (predicting clean data from noisy), and the forward-backward SDE formulation. The core insight is that generation is time-reversed diffusion. Song et al. (S21, arXiv 2011.13456) made the stochastic calculus explicit: the forward process is Ornstein--Uhlenbeck; the reverse process requires the score function, learned by the neural network. Sampling from a diffusion model is Langevin dynamics on the data distribution.

The connection to stochastic quantization is immediate and mathematically precise. Both diffusion model sampling and stochastic quantization involve learning or computing drift terms for Langevin dynamics. The tools are the same: Ito calculus, Fokker--Planck equations, score matching. The target differs---a data distribution for diffusion models, a quantum path integral measure for stochastic quantization---and practical differences in gauge structure, complex actions, and discretization choices matter enormously in the QFT context. But the mathematical machinery is shared, and techniques developed in one domain can inform the other.

Sohl-Dickstein et al. (S52, arXiv 1503.03585) provide the historical precursor, drawing explicit parallels to nonequilibrium thermodynamics, the Jarzynski equality, and nonequilibrium work fluctuations. The forward diffusion increases entropy; the learned reverse process decreases it.

S25 (arXiv 2010.00029) interprets RG steps as unsupervised normalizing flows, showing that the coarse-graining transformation of real-space RG can be learned as a flow providing both dimension reduction and density estimation simultaneously. This connects the generative modeling program back to the RG themes of Sections 8 and 9.

Three broad classes of generative models emerge from this section, each with different computational strengths: likelihood-based density models (flows, autoregressive models) that provide exact density evaluation; implicit models (GANs) that provide fast sampling but no density; and diffusion/score models that provide flexible sampling through stochastic dynamics. The physics perspective suggests that these correspond to different computational strategies for the same underlying problem: sampling from a target distribution defined by a complicated energy landscape.


## 11. Approximate Inference and Normalising Flows

Bishop-24 Chapter 7 covers the optimization toolkit: SGD, Adam, learning rate schedules, momentum, and initialization strategies. Murphy-23 Chapters 7, 10, and 23 treat inference foundations, variational Bayes (mean-field and structured approximations), and modern normalizing flows. Goodfellow-16 Chapters 8 and 19 address optimization and energy-based models.

The supplementary readings develop the theme of inference as dynamics. Chen et al. (S17, arXiv 1806.07366) introduced neural ODEs, treating network depth as a continuous variable. The key observation is that residual networks---networks of the form $x_{t+1} = x_t + f(x_t, \theta)$---approximate ODE solutions. In the limit of infinitesimally small residual steps, they become exact: the network output is the solution of an ODE at final time. This makes the dynamical systems perspective rigorous: depth is time, the residual function is the vector field, and forward propagation is numerical integration.

The practical consequences are substantial. Neural ODEs enable adaptive computation (the ODE solver chooses its own step sizes), memory-efficient backpropagation (via the adjoint method, which avoids storing intermediate activations), and continuous normalizing flows (where the change-of-variables formula involves a trace rather than a determinant). The connection to optimal control theory is also precise: training a neural ODE is equivalent to optimal control of the vector field.

S40 (arXiv 1603.01880) provides a cautionary counterpoint: neural ODEs can exhibit chaos. Continuous-depth networks with positive Lyapunov exponents display sensitive dependence on initial conditions, and the adjoint method accumulates errors exponentially in chaotic regimes. Understanding when neural ODEs are stable requires the same stability analysis used for physical dynamical systems.

The Hamiltonian and Lagrangian neural networks from Section 5 (S31--S34) reappear here as volume-preserving flows for Bayesian inference. Hamiltonian flows preserve phase space volume (Liouville's theorem), making them natural candidates for normalizing flow design and for MCMC proposal mechanisms. S41 (Physical Review E 98, cross-referenced from Section 5) connects path-integral methods to the approximate posterior dynamics of wide networks, where the variational approximation corresponds to mean-field and systematic improvements correspond to including higher-order diagrams.


## 12. Sampling and Monte Carlo Methods

Bishop-24 Chapter 14 covers Metropolis--Hastings, slice sampling, Gibbs sampling, and Hamiltonian Monte Carlo (HMC). Murphy-23 Chapters 11--13 provide the full modern treatment: Monte Carlo integration foundations, adaptive MCMC including NUTS (No-U-Turn Sampler), and sequential Monte Carlo (particle filters).

MCMC is the computational backbone of Bayesian inference and, by extension, of stochastic quantization. HMC makes the physics connection explicit: sampling from a target distribution $\pi(q)$ is equivalent to simulating Hamiltonian dynamics in an extended phase space $(q, p)$ with potential energy $U(q) = -\log \pi(q)$ and kinetic energy $K(p) = p^2/2m$. The dynamics are volume-preserving (Liouville) and time-reversible, ensuring detailed balance. NUTS automates the tuning of trajectory length, removing the main practical obstacle to HMC deployment.

The two supplementary references bracket the field's development. Andrieu et al. (S15, 2003) provide the classic MCMC-for-ML tutorial---still worth reading for its clarity and completeness. The modern review (S16, arXiv 2402.09598) updates the toolkit with stochastic gradient MCMC (SGLD, SGHMC) for scaling to large datasets, neural network--enhanced samplers (learned proposals, normalizing flow MCMC), and the NUTS algorithm.

The modern review is important because it documents the convergence between MCMC and deep learning: neural networks are being used to design better MCMC kernels, while MCMC provides the sampling infrastructure for Bayesian neural network training. For stochastic quantization research, this section provides the practical algorithms for sampling path integral measures, and the Langevin dynamics underlying SGLD is precisely the stochastic dynamics that stochastic quantization exploits.


## 13. Sequence and Time-Series Learning

Goodfellow-16 Chapter 10 covers RNN fundamentals. Bishop-24 Chapter 12 treats transformers and self-attention. Murphy-23 Chapter 8 covers Kalman filters and linear dynamical systems; Chapter 29 addresses modern state-space networks including structured state spaces (S4 architecture) and Mamba. The classical treatment (Kalman) connects to control theory; the modern treatment (transformers, state-space models) provides the architectures.

The supplementary readings (S57--S64) constitute the most application-heavy section of the notes, demonstrating the full ML pipeline for gravitational wave science and numerical relativity. The collection is organized as a coherent workflow.

**Detection and characterization.** S57 (Cardiff 2015) pioneers CNN inference on raw gravitational-wave time series, demonstrating that ML can match or beat matched filtering for signal detection. S58 (arXiv 1710.07092) applies HMMs for continuous gravitational wave tracking from persistent sources such as mountains on neutron stars. S59 (arXiv 1911.09083) deploys deep sequence networks to reduce detection latency for electromagnetic follow-up alerts.

**Surrogate modeling and forward evolution.** S60 (arXiv 2001.02515) shows that RNNs can emulate the evolution of the Einstein equations, learning the mapping from initial data to evolved spacetime. S61 (arXiv 2110.08901) builds surrogate models for gravitational waveforms, enabling rapid template generation for parameter estimation without expensive numerical relativity simulations. S63 (arXiv 2201.01644) learns exact GR solutions using physics-informed neural networks, solving the Einstein equations as a supervised learning problem.

**Signal processing and compression.** S62 (IOP 2021) combines spectrogram preprocessing with CNN classifiers for gravitational wave burst detection from unmodeled sources. S64 (arXiv 2210.07299) compresses full numerical relativity waveforms with autoencoding, achieving approximately two orders of magnitude in storage reduction while preserving physical accuracy.

The pipeline is coherent: detection and characterization at the data interface, surrogate modeling to replace expensive simulations, and compression for storage and transmission. It provides a template for applying ML to other scientific domains where the workflow involves expensive forward models, noisy data, and the need for real-time or near-real-time inference.

For the broader themes of these notes, the state-space formulation (Murphy-23 Chapter 29) is particularly relevant. The hidden state in a state-space model is analogous to the field configuration at intermediate times in a path integral; marginalization over hidden states is analogous to the path integral itself. Sequence learning, viewed through this lens, is path-integral computation---a connection that links the applied work in gravitational wave science to the theoretical framework of Sections 8 and 10.


## 14. Decision-Making, Causality, and Frontier Topics

Murphy-23 Chapters 33--36 cover interpretability, decision theory, reinforcement learning, and causal inference. Goodfellow-16 Chapters 11--12 provide engineering methodology and application case studies.

The two supplementary references complete the intellectual circle. S38 (arXiv 2309.01909) demonstrates reinforcement learning with physics constraints, incorporating conservation laws into reward structures and policy architectures. S53 (arXiv 1906.10228) provides the statistical physics perspective on RL: the trajectory distribution in RL is interpreted as a Boltzmann distribution over action sequences, with the reward function playing the role of negative energy. The optimal policy is the ground state of the corresponding system in the zero-temperature limit. This provides the theoretical foundation for entropy-regularized RL (soft actor-critic) and maximum-entropy approaches.

If supervised learning corresponds to inference in a statistical field theory, reinforcement learning corresponds to optimization over trajectory distributions in that theory. The trajectory distribution is a path integral measure over action sequences; the optimal policy is the saddle point. Physics-constrained RL (S38) shows how to build conservation laws into practical algorithms, extending the symmetry-aware architecture principles of Section 5 to sequential decision-making.


## Cross-Cutting Themes

Several themes run through the entire bibliography, appearing in different guises across the fourteen sections.

**The probabilistic spine.** Machine learning, as presented in these notes, is fundamentally about inference in probability distributions. The textbooks---especially Murphy (2022, 2023)---provide the systematic framework: priors, likelihoods, posteriors, predictive distributions, decision rules. This is not one perspective among many; it is the organizing principle. Every architecture encodes a prior. Every loss function specifies a likelihood. Every training run is approximate inference. Every prediction is a posterior expectation (or an approximation to one). The probabilistic framework provides the language in which the physics connections become precise.

**The physics interface.** The supplementary readings repeatedly interpret ML objects through the lens of statistical physics. Loss functions are energies. Ensembles of networks are statistical mechanical systems. Wide-network limits are Gaussian (free field) theories. Finite-width corrections are interactions. Regularization modifies the action. Training dynamics are relaxation processes. This provides a coherent meta-narrative linking seemingly disparate topics: the same mathematical structures that govern regularization (Section 7), kernels (Section 6), diffusion (Section 10), and the NN--QFT correspondence (Section 8) are all manifestations of inference in energy-based models.

**Dynamics everywhere.** Sections 10--12 emphasize that modern generative modeling and Bayesian computation can be expressed as stochastic dynamics. Score-based diffusion models solve reverse-time SDEs. Normalizing flows solve ODEs. HMC simulates Hamiltonian dynamics. SGD is (approximately) Langevin dynamics with learning rate as temperature. The same Ito calculus, Fokker--Planck equations, and path integral formulations appear in all of these contexts. This makes the bibliography unusually well-aligned with readers who work with SDEs, Langevin dynamics, and path integrals in other settings---and it makes the connection to stochastic quantization essentially automatic.

**Numerical relativity as a capstone domain.** Section 13 grounds the theoretical framework in a concrete scientific workflow. Gravitational wave science is an application domain where the full pipeline is visible: detection from noisy time series, characterization via statistical inference, forward modeling through surrogates of the Einstein equations, and compression for storage. The domain is computationally demanding (motivating ML surrogates), physically constrained (motivating physics-informed architectures), and data-rich (motivating deep learning approaches). It provides a worked example of the principles developed throughout the notes.


## Open Questions

The bibliography, reveals unsettled considerations and open questions.

**Training dynamics.** Most field-theoretic results concern initialization distributions or equilibrium properties. The correspondence for SGD dynamics at finite learning rate is incomplete. The noise in SGD is not Gaussian, the implicit regularization is not fully understood, and the relationship between the "trained" distribution and the "equilibrium" distribution of the field theory is unclear.

**Finite-width effects.** The perturbative expansion in inverse width is understood at leading order, but strongly-coupled (narrow) networks remain challenging, just as strongly-coupled QFTs are. Most practical networks operate well outside the regime where perturbation theory is reliable.

**Structured and discrete data.** The field-theoretic framework is most natural for continuous inputs. Extension to discrete, combinatorial, or graph-structured data requires tensor field generalizations that are less developed.

**Empirical validation.** Many theoretical predictions---scaling with depth-to-width ratio, universality classes for different activations, critical exponents at the edge of chaos---await systematic experimental confirmation in practical training regimes. The theory describes ensembles; practice trains single networks.

**Integration with practice.** How to use the NN--QFT perspective to improve practical engineering of large-scale models remains an open question. The theoretical framework provides explanatory power; its prescriptive power for architecture design and training is still being developed.


## Summary

These notes have traced a path through the machine learning literature organized by a single thesis: that neural networks are statistical mechanical systems whose behavior can be understood through the mathematical tools of field theory, stochastic dynamics, and renormalization. The five textbooks (Bishop 2006/2024, Goodfellow 2016, Murphy 2022/2023) provide the standard curriculum. The sixty-four supplementary readings develop the field-theoretic perspective and its applications to physics.

The intellectual payoff is a set of precise correspondences: loss functions and energies; network ensembles and field theories; wide-network limits and free field theories; finite-width corrections and interactions; regularization and action modification; dimensionality reduction and coarse-graining; generative sampling and Langevin dynamics; reinforcement learning and path-integral optimization. These identifications are mathematical in character, valid in the limits where they have been rigorously established and plausibly extending beyond those limits.

For the practitioner, these correspondences provide tools: perturbation theory for computing finite-width corrections, random matrix theory for analyzing kernel spectra, the RG equation for understanding how learned representations change with scale. For the theorist, they provide problems: extending the correspondence beyond the perturbative regime, understanding training dynamics as a genuinely nonequilibrium process, and connecting the ensemble theory to single-network behavior. For both, the stochastic dynamics---Langevin equations, Fokker--Planck equations, path integrals---that appear in diffusion models, MCMC, neural ODEs, and stochastic quantization constitute a shared mathematical language that makes the boundaries between "machine learning" and "physics" increasingly difficult to locate.


### Textbooks
* **Bishop-06** [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/wp-content/uploads/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf), 
* **Goodfellow-16** [Deep Learning](https://www.deeplearningbook.org), 
* **Murphy-22** [Probabilistic Machine Learning-Intro](https://probml.github.io/pml-book/book1.html), 
* **Murphy-23** [Probabilistic Machine Learning-Adv](https://probml.github.io/pml-book/book2.html), and 
* **Bishop-24** [Deep Learning: Foundations and Concepts](https://www.bishopbook.com).
* External hyper-linked references = S1 … S64


## Overview

### Chapters

* **Bishop-24 Ch 1** – Historical tour with modern DL vocabulary.
* **Goodfellow-16 Ch 1** – Frames DL as the third wave of AI.
* **Murphy-22 Ch 1 & Ch 5** – Rational decision-making in uncertain worlds.
* **Murphy-23 Ch 1** – Overview of the landscape.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S1  | [arXiv 1301.7115](https://arxiv.org/abs/1301.7115)                             | Early deep-learning breakthroughs.   |
| S2  | [arXiv 1803.08823](https://arxiv.org/abs/1803.08823)                           | Gives physicists a lay-of-the-land tour of ML. |
| S4  | [arXiv 1903.10563](https://arxiv.org/abs/1903.10563)                           | Surveys DL’s adoption across the physical sciences.         |
| S5  | [Springer book 2020](https://link.springer.com/book/10.1007/978-3-030-40245-7) | Quantum physics DL research.                     |
| S7  | [Nature Phys 2020](https://www.nature.com/articles/s41567-020-0929-2)          | Snapshot geared toward a physics readership.                            |
| S8  | [arXiv 2104.03902](https://arxiv.org/abs/2104.03902)                           | Speculates on a universe that trains itself.    |
| S9  | [arXiv 2104.00008](https://arxiv.org/abs/2104.00008)                           | AI & physics on a single timeline.                   |
| S11 | [arXiv 2408.00082](https://arxiv.org/abs/2408.00082)                           | TASI lectures as conceptual gateway.                                     |

---

## Probability & Statistical Foundations

### Chapters

* **Bishop-24 Ch 2–3** – Bayes, KL-divergence and catalogue of common distributions.
* **Goodfellow-16 Ch 2–4** – Linear algebra, probability, information.
* **Murphy-22 Ch 2-4 & 6** – Univariate & multivariate probability. Linear algebra.
* **Murphy-23 Ch 2–3 & 5** – Condensed reiteration.
* **PRML-06 App B–C** – Reference tables for distributions and matrix identities.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S22 | [arXiv cond-mat/9607180](https://arxiv.org/abs/cond-mat/9607180) | Re-derives priors from maximum-entropy field theory.   |
| S23 | [arXiv cond-mat/0009165](https://arxiv.org/abs/cond-mat/0009165) | Extends the field-theoretic argument to dynamic data.            |
| S24 | [PubMed 25018724](https://pubmed.ncbi.nlm.nih.gov/25018724/)     | Neuroscience model averaging parameter uncertainty.         |
| S26 | [arXiv 2112.01388](https://arxiv.org/abs/2112.01388)             | Residual-prior pipeline for deep nets with resilience of theoretical priors to engineering.    |
| S27 | [arXiv 2305.10491](https://arxiv.org/abs/2305.10491)             | Renormalisation and Bayesian evidence. |

---

## Linear Regression & Generalised Linear Models

### Chapters

* **Bishop-24 Ch 4** – Single-layer network ordinary least squares.
* **Murphy-22 Ch 8 & 12** – From homoskedastic Gaussian models to Poisson/Bernoulli GLMs.
* **Murphy-23 Ch 15** – Asymptotic statistical treatment of GLM inference.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S12 | [arXiv 1702.01522](https://arxiv.org/abs/1702.01522) | Converts inverse-Ising physics into penalised linear regression. |

---

## Linear Classification

### Chapters

* **Bishop-24 Ch 5** – Logistic-sigmoid networks and soft-max regression.
* **Murphy-22 Ch 9–10** – Fisher-LDA and logistic regression foundations.

### Applications & Illustrations

---

## Neural Networks & Deep Learning

### Chapters

* **Bishop-24 Ch 6, 8, 10** – Multilayer perceptrons, back-prop,  and CNNs.
* **Goodfellow-16 Ch 6–9** – Deep feed-forward, regularisation,  and convolutional networks.
* **Murphy-22 Ch 11–13** – MLP, CNN and sequence nets.
* **Murphy-23 Ch 16–17** – Very-deep architectures and Bayesian NNs.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S6  | [arXiv 2008.01540](https://arxiv.org/abs/2008.01540)                              | Argues cosmological simulation encoded as NN. Underscores expressive power.      |
| S7  | [Nature Phys 2020](https://www.nature.com/articles/s41567-020-0929-2)             | Gives physicists an architect’s view of DL layers. Complements Goodfellow’s engineering view.        |
| S10 | [arXiv 2301.00942](https://arxiv.org/abs/2301.00942)                              | Solves computational-physics PDEs with generic DNNs. Depth pays off in science workloads.       |
| S28 | [arXiv 1906.02481](https://arxiv.org/abs/1906.02481) | Elevates CNN into equivariant spaces. |
| S29 | [arXiv 2002.12880](https://arxiv.org/abs/2002.12880)                              | CNNs expanded to Lie-group symmetries. See Bishop’s translation-equivariance. |
| S30 | [arXiv 2104.13478](https://arxiv.org/abs/2104.13478)                              | Geometric DL road maps connecting CNN to manifolds and graphs.                      |
| S31 | [arXiv 1906.01563](https://arxiv.org/abs/1906.01563)                              | Embeds Hamiltonian mechanics injecting physics priors into deep feed-forward models.   |
| S32 | [arXiv 2010.13581](https://arxiv.org/abs/2010.13581)                              | Extends Hamiltonian nets to higher-order systems, pushing physics-aware architectures.          |
| S33 | [arXiv 2003.04630](https://arxiv.org/abs/2003.04630)                              | Neural networks via Lagrangian dynamics.             |
| S34 | [arXiv 2202.04836](https://arxiv.org/abs/2202.04836)                              | Adds constraint handling to Hamiltonian NNs. Robotics and molecule simulation.               |
| S35 | [Nature Rev Phys 2021](https://www.nature.com/articles/s42254-021-00314-5)        | Reviews of physics-informed DL field. Domain priors.X-IML                   |
| S36 | [arXiv 2203.16797](https://arxiv.org/abs/2203.16797)                              | Recipes for engineering PIML systems.                                            |
| S37 | [arXiv 2304.14994](https://arxiv.org/abs/2304.14994)                              | U-Nets as neural surrogates for expensive PDE solvers.                                |
| S41 | [Phys Rev E 98](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.98.062120) | Path integral analysis of wide-network learning trajectories. |
| S43 | [arXiv 1910.00019](https://arxiv.org/abs/1910.00019)                              | Neural tangent kernel theory for infinite-width MLPs.                           |

---

## Kernel Methods & Gaussian Processes

### Chapters

* **Murphy-22 Ch 17** – SVMs, kernel trick and kernel ridge.
* **Murphy-23 Ch 18** – Full Bayesian treatment of Gaussian processes.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S19 | [RMT4ML notes 2023](https://zhenyu-liao.github.io/pdf/RMT4ML.pdf) | Pedagogy-first walk through of RMT diagnosis of kernel learning dynamics.                    |

---

## Regularisation & Ensemble Learning

### Chapters

* **Goodfellow-16 Ch 7** – Dropout, L1/L2, data augmentation.
* **Bishop-24 Ch 9** – Modern view: batch-norm, residual paths, double-descent.
* **Murphy-22 Ch 16 & 18** – k-NN sparsity plus tree/boosting ensembles.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S13 | [StatMechDeep PDF](https://ganguli-gang.stanford.edu/pdf/20.StatMechDeep.pdf)         | Free-energy landscapes view of regularisation.                                     |
| S14 | [Physica A 2023](https://www.sciencedirect.com/science/article/pii/S0378437122007129) | Penalties sculpting loss surfaces.   
| S18 | [arXiv 2306.02108](https://arxiv.org/abs/2306.02108)              | Random-matrix theory of landscape of loss surfaces|                  |
| S56 | [arXiv 1709.02470](https://arxiv.org/abs/1709.02470)                                  | Double-descent and phase-transitions theory. Statistical-physics view of ensembles. |

---

## Graphical Models & Structured Probability

### Chapters

* **Bishop-24 Ch 11** – Factor graphs, HMMs, autoregressive densities.
* **Murphy-23 Ch 4 & 30** – Modern structure-learning and graph inference.
* **PRML-06 Ch 8–10** – The classic directed + undirected PGM treatment.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S42 | [arXiv 1901.10416](https://arxiv.org/abs/1901.10416)                                               | Statistical field theory methods and deep nets. |
| S44 | [Springer SFT-NN 2020](https://link.springer.com/book/10.1007/978-3-030-46444-8)                   | Monograph-length bridge between field theory and deep nets.                         |
| S45 | [arXiv 2109.13247](https://arxiv.org/abs/2109.13247)                                               | Reviews DL–QFT correspondence.                                         |
| S46 | [arXiv 2106.10165](https://arxiv.org/abs/2106.10165)                                               | Effective-field theory methods I.                                |
| S47 | [arXiv 2008.08601](https://arxiv.org/abs/2008.08601)                                               | Effective-field theory methods II.                   |
| S48 | [arXiv 2102.09449](https://arxiv.org/abs/2102.09449)                                               | QFTs as NN.                          |
| S49 | [arXiv 1812.09345](https://arxiv.org/abs/1812.09345)                                               | MSRJD and Onsanger Machlup.         |
| S50 | [arXiv 2212.11811](https://arxiv.org/abs/2212.11811)                                               | Renormalization and group flows.                       |
| S51 | [arXiv 2108.01403](https://arxiv.org/abs/2108.01403)                                               | RG acting as a hierarchy of probabilistic graphs.                              |

---

## Dimensionality Reduction & Latent Variables

### Chapters

* **Bishop-24 Ch 16 & 19** – PCA, FA, ICA and autoencoders/VAEs.
* **Goodfellow-16 Ch 13–14** – Linear factor models and AEs in DL style.
* **Murphy-22 Ch 20** – t-SNE, Isomap, kernel PCA.
* **Murphy-23 Ch 27–28, 32** – Discovery & representation learning.

### Applications & Illustrations


| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S54 | [arXiv 1610.09733](https://arxiv.org/abs/1610.09733) | PCA spectra RG flows: dimensionality reduction and scale-finding. |
| S55 | [J. Stat. Phys. 2017](https://link.springer.com/article/10.1007/s10955-017-1770-6) | Includes biological and financial data. |

---

## Deep Generative Models

### Chapters

* **Bishop-24 Ch 15, 17, 18, 20** – Discrete latents, GANs, flows and diffusion.
* **Goodfellow-16 Ch 20** – Early 2016 survey of deep generators.
* **Murphy-23 Ch 20–26** – Probabilistic view of VAEs, GANs, and Diffusion.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S3 | [PIL tutorial PDF](https://wangleiphy.github.io/lectures/PILtutorial.pdf) | VAEs and denoising AEs. Code example tutorial |
| S20 | [arXiv 2006.11239](https://arxiv.org/abs/2006.11239) | Invents DDPMs. |
| S21 | [arXiv 2011.13456](https://arxiv.org/abs/2011.13456) | Score-based SDE sampling and Itô calculus. |
| S25 | [arXiv 2010.00029](https://arxiv.org/abs/2010.00029) | RG steps as an unsupervised flow. |
| S52 | [arXiv 1503.03585](https://arxiv.org/abs/1503.03585) | Early nonequilibrium: Foreshadows modern score-matching diffusions. |

---

## Approximate Inference & Normalising Flows

### Chapters

* **Bishop-24 Ch 7** – SGD, Adam, line-search, initialisation.
* **Murphy-23 Ch 7, 10 & 23** – Inference overview, variational Bayes, modern flows.
* **Goodfellow-16 Ch 8 & 19** – Optimisation details. Deep energy models.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S17 | [arXiv 1806.07366](https://arxiv.org/abs/1806.07366) | Neural ODEs. Continuous-time optimisation and invertible flows. |
| S31–S34 | see §5 | Hamiltonian/Lagrangian NNs as volume-preserving flows for Bayesian inference. |
| S40 | [arXiv 1603.01880](https://arxiv.org/abs/1603.01880) | Chaos in neural ODE training. Queries flow stability. |
| S41 | [Phys Rev E 98](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.98.062120) | Path-integral methods to approximate posterior dynamics of wide nets. |

---

## Sampling & Monte-Carlo Methods

### Chapters

* **Bishop-24 Ch 14** – Metropolis, slice, Gibbs, HMC.
* **Murphy-23 Ch 11–13** – MC integration, adaptive MCMC, SMC.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S15 | [Andrieu et al. 2003](https://www.cs.ubc.ca/~arnaud/andrieu_defreitas_doucet_jordan_intromontecarlomachinelearning.pdf) | Classic tutorial. |
| S16 | [arXiv 2402.09598](https://arxiv.org/abs/2402.09598) | Modern review: Updates Bishop’s 2006 toolkit. |

---

## Sequence & Time-Series Learning

### Chapters

* **Goodfellow-16 Ch 10** – RNN fundamentals.
* **Bishop-24 Ch 12** – Transformers and self-attention.
* **Murphy-23 Ch 8 & 29** – Kalman/LDS and modern state-space nets.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S57 | [Cardiff 2015](https://orca.cardiff.ac.uk/id/eprint/90458/) | Pioneers CNN inference on raw gravitational-wave time series. Beats matched filtering. |
| S58 | [arXiv 1710.07092](https://arxiv.org/abs/1710.07092) | Uses HMMs for continuous GW tracking. Mirrors hidden-state example. |
| S59 | [arXiv 1911.09083](https://arxiv.org/abs/1911.09083) | Deploys DL sequence nets to reduce GW detection latency. |
| S60 | [arXiv 2001.02515](https://arxiv.org/abs/2001.02515) | RNNs can emulate evolution of Einstein equations. |
| S61 | [arXiv 2110.08901](https://arxiv.org/abs/2110.08901) | Builds surrogates GW waveforms. |
| S62 | [IOP 2021](https://iopscience.iop.org/article/10.1088/2632-2153/abb93a) | Combines spectrogram preprocessing with CNN classifiers for GW bursts. |
| S63 | [arXiv 2201.01644](https://arxiv.org/abs/2201.01644) | Learns exact GR solutions. |
| S64 | [arXiv 2210.07299](https://arxiv.org/abs/2210.07299) | Compresses full numerical-relativity waveforms with autoencoding, reducing storage 100×. |

---

## Decision-Making, Causality & Frontier Topics

### Chapters

* **Murphy-23 Ch 33–36** – Interpretability, decision theory, RL and causal inference.
* **Goodfellow-16 Ch 11–12** – Practical methodology and application case-studies.

### Applications & Illustrations

| ID  | Link                                                                                               | Notes                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| S38 | [arXiv 2309.01909](https://arxiv.org/abs/2309.01909)                              | Reinforcement learning with physics constraints.                 |
| S53 | [arXiv 1906.10228](https://arxiv.org/abs/1906.10228) | Statistical physics view of RL. |

---

