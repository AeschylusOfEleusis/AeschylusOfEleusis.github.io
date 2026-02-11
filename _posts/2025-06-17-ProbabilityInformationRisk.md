---
layout:   post
title: "Probability, Information and Risk"
date: 2025-06-17 10:00:00 +0800
categories: [Computational Finance]
tags: [Machine Learning, Computational Finance, Stochastic Calculus, Fractional Calculus, Scientific Computing, Quantum Computing]
math:       true        # enable KaTeX
---
# Notes on Probability, Information, & Risk  (Draft)

## Abstract

Research notes are provided concerning three interconnected subjects---probability, information, and risk---that together form a coherent intellectual arc from foundational mathematics to sequential decision-making under uncertainty. Both frequentist and Bayesian interpretations of probability are considered, beginning with Kolmogorov's measure-theoretic axioms and extending through Jaynes's reinterpretation of probability as logic, with application in Grenander and Mumford's Pattern Theory. The treatment of information encompasses Shannon's general theory, algorithmic complexity in the sense of Chaitin and Kolmogorov, geometric perspectives on statistical manifolds, and physical interpretations connecting entropy to thermodynamics and the theory of computation. The section on risk considers the mathematics of games and gambling, centering on the information-theoretic Kelly criterion as developed and advocated by E. O. Thorp. Twenty-eight primary sources are surveyed. 

**Keywords:** probability theory, Bayesian inference, Shannon entropy, information geometry, Kelly criterion, stochastic processes, algorithmic information theory, risk management

---

## 1. Introduction

These notes belong to a broader collection of research notes for *Projects in Scientific Computating*. The method employed throughout is  "writing toward understanding"---the composition of notes that are simultaneously acts of learning and acts of exposition. The result is neither a textbook nor a review article in the conventional sense, but something in between: a  guide to the literature and a mirror of the structure of the subject considered. The notes survey twenty-eight sources across three domains, providing the kind of bibliographic depth and commentary that standard references typically condense into a few sentences of "further reading."

The three subjects treated here---probability, information, and risk---are not independent. They form a logical progression that reflects genuine historical and mathematical entanglement. Probability theory provides the measure-theoretic and logical foundations for reasoning under uncertainty. Information theory, born from Shannon's work at Bell Labs in 1948, quantifies that uncertainty and establishes fundamental limits on communication, compression, and inference. Risk theory---here considered primarily through the lens of games, gambling, and the Kelly criterion---translates both probability and information into sequential decision-making: how to size bets, manage capital, and exploit an edge over time.

The connecting thread is entropy. Shannon entropy $H(X) = -\sum p(x_i) \log p(x_i)$ appears first as a measure of uncertainty in a probability distribution, then as the fundamental quantity in coding theory and channel capacity, and finally (through Kelly's criterion) as the objective function for growth-optimal betting. Kelly was Shannon's colleague at Bell Labs; his criterion maximizes expected logarithmic wealth, which is equivalent to maximizing the rate of information transmission in a gambling channel. This is not a superficial analogy but a precise mathematical correspondence.

The notes are organized in three parts. Part I surveys the probability literature from Kolmogorov's 1933 axioms through modern stochastic process theory. Part II traces information theory from Shannon through algorithmic complexity, information geometry, and the physics of computation. Part III examines risk through the mathematics of gambling and the Kelly capital growth criterion. A synthesis section discusses how the three threads weave together and identifies natural learning paths through the material.

A note on level: the sources surveyed range from accessible introductions (DeDeo, Pierce, Bollman) to graduate-level texts (Grimmett and Stirzaker, Cover and Thomas) to research-level papers (Ciaglia et al., Wolpert). The bibliography is selective and personal---it does not aim to be exhaustive, but it is coherent in its arc. Several entries point to freely accessible PDFs, which substantially lowers the activation energy for self-study.

---

## Part I: Probability

### 2. Overview: Two Views of Probability

The foundations of probability admit two broad philosophical interpretations, both of which are represented in this collection. The frequentist view, formalized by Kolmogorov in 1933, treats probability as a mathematical structure: a normalized, countably additive measure on a $\sigma$-algebra of events. The Bayesian view, championed by Jaynes and developed operationally by DeDeo, treats probability as a logic of plausible reasoning---degrees of belief constrained by consistency requirements.

These views are not mutually exclusive in practice. The measure-theoretic framework provides the rigorous infrastructure (convergence theorems, conditioning, martingales) needed for stochastic processes and mathematical finance. The Bayesian interpretation provides the conceptual scaffolding for inference problems where one must reason from incomplete information to conclusions about the world. A working scientist needs both.

The probability section of these notes surveys six sources arranged along two axes: from foundational to applied, and from frequentist to Bayesian. The arc begins with Kolmogorov's axioms, passes through Jaynes's philosophical reinterpretation, illustrates Bayesian modeling on structured spaces through Mumford's Pattern Theory, provides an accessible operational introduction via DeDeo, and concludes with the heavy-duty stochastic process machinery of Grimmett and Stirzaker that supports the risk section's repeated-game and long-run arguments.

### 3. Kolmogorov's Foundations

**S1: Kolmogorov, *Foundations of the Theory of Probability* (1933; English 2nd ed. 1956)**

The original German monograph *Grundbegriffe der Wahrscheinlichkeitsrechnung* established probability as a branch of measure theory. Before Kolmogorov, probability was a collection of techniques---combinatorial arguments, limit theorems, characteristic functions---that lacked a unified logical foundation. Kolmogorov's contribution was to identify the essential structure: a probability space $(\Omega, \mathcal{F}, P)$ consisting of a sample space, a $\sigma$-algebra of events, and a countably additive measure normalized to unity.

The consequences of this axiomatization are far-reaching. Random variables become measurable functions $X: \Omega \to \mathbb{R}$. Expectation becomes a Lebesgue integral. Independence receives a precise definition in terms of product measures. Conditional expectation becomes a measurable function (not merely a ratio of probabilities), defined through the Radon-Nikodym theorem. The various modes of convergence---almost sure, in probability, in distribution, in $L^p$---acquire their proper relationships.

For the present notes, the key point is that Kolmogorov's framework provides the infrastructure needed for everything that follows: stochastic processes (Part I), information-theoretic quantities defined on probability distributions (Part II), and the almost-sure convergence results that underpin the Kelly criterion (Part III).

The English translation remains available as a PDF and is worth reading for its concision. At roughly 80 pages, it is a model of mathematical economy. The reader trained in real analysis will find the arguments transparent; the reader without such training will need to supplement with a measure theory text (Billingsley's *Probability and Measure* is the standard recommendation).

### 4. Probability as Logic: Jaynes and the Bayesian Program

**S2: Jaynes, *Probability: The Logic of Science* (2003)**

Jaynes's posthumously published treatise represents the most sustained argument for the Bayesian interpretation of probability as an extension of deductive logic to situations involving incomplete information. Where Kolmogorov asks "what is the mathematical structure of probability?", Jaynes asks "what rules must any consistent agent follow when reasoning under uncertainty?" The answer, derived from Cox's theorem, is that the rules of probability theory are the unique consistent extension of Boolean logic to continuous degrees of plausibility.

This is a philosophical claim with mathematical consequences. If probabilities represent degrees of belief rather than limiting frequencies, then Bayes's theorem is not merely a formula but the fundamental rule of inference:

$$P(H \mid D) = \frac{P(D \mid H) \, P(H)}{P(D)}$$

The posterior probability of a hypothesis $H$ given data $D$ is determined by the likelihood $P(D \mid H)$, the prior $P(H)$, and the evidence $P(D)$. The choice of prior is not arbitrary but constrained by symmetry arguments, transformation groups, and the principle of maximum entropy.

Jaynes's maximum entropy principle is particularly relevant for the information theory section: when assigning a probability distribution subject to constraints (known expectation values, for instance), one should choose the distribution that maximizes Shannon entropy subject to those constraints. This principle connects Bayesian inference directly to statistical mechanics---the canonical and microcanonical ensembles emerge as maximum entropy distributions under energy and particle-number constraints.

The excerpt available online covers the foundational chapters: the philosophy of plausible reasoning, the derivation of probability rules from desiderata, and the beginnings of the maximum entropy program. The full text extends to detailed applications in physics, including the resolution of various "paradoxes" that Jaynes attributes to confused reasoning about priors.

Two caveats are worth noting. First, Jaynes writes polemically. His arguments against frequentism are often more rhetorical than necessary, and readers from a measure-theoretic background may find the dismissive tone unproductive. Second, the book was unfinished at Jaynes's death in 1998 and completed by G. Larry Bretthorst; the later chapters are less polished than the earlier ones.

### 5. Bayesian Modeling on Structured Spaces

**S3: Mumford and Desolneux, *Pattern Theory* (2010)**

If Jaynes provides the philosophical argument for Bayesian probability, Mumford and Desolneux provide one of its most sophisticated applications. Pattern Theory, in the Grenander school, treats perception and inference as Bayesian computation on structured hypothesis spaces: graphs, templates, grammars, and hierarchical compositions.

The central idea is that natural signals---images, text, speech---are samples from probability models defined over rich combinatorial and geometric spaces. A Markov random field on a lattice generates texture. A deformable template generates faces. A stochastic grammar generates sentences. Inference consists of computing posterior distributions over these structured representations given observed data.

The Brown University course site provides chapter-level materials and exercises. Representative topics include Markov chains on English text, Gibbs random fields for image texture, flexible templates for faces, and multiscale analysis of natural scenes. For the reader coming from physics, the Gibbs/Boltzmann distributions on lattice configurations will be immediately familiar; the novelty is in the application to perceptual and cognitive problems.

Within the present bibliography, Pattern Theory serves as a concrete demonstration that Bayesian probability becomes powerful when the hypothesis space has rich structure. It also provides a bridge toward information-theoretic perspectives: good probabilistic models compress data, and the connection between compression and prediction is a central theme of MacKay's text in Part II.

### 6. Operational Bayesian Reasoning

**S4: DeDeo, *Bayes for Intelligent People* (2018)**

DeDeo's notes are a concise, readable introduction to Bayesian reasoning aimed at mathematically literate readers who want operational understanding rather than philosophical argument. The document covers the core identity $P(x,y) = P(x \mid y)P(y) = P(y \mid x)P(x)$, derives Bayes's theorem, and works through several memorable examples.

Among these: the Madame Blavatsky ESP example (after Jaynes), which illustrates how prior probabilities can overwhelm likelihoods; Hume's argument against miracles recast as a prior-probability argument; Aumann's agreement theorem, which constrains persistent disagreement between rational agents with common priors; and a detailed worked example on waiting for the Number 55 bus that connects Bayesian updating to stochastic process intuition through reflection principles for Brownian motion.

The notes also address the problem of quantifying beliefs via betting odds, including Keynes's objections and Searle's counterexamples. This thread connects to the risk section: if probability represents willingness to bet, then the Kelly criterion provides the optimal way to translate belief into action.

DeDeo's companion document on information theory (S14, discussed in Part II) forms a natural pair with these notes. Together they provide an accessible entry point to the probabilistic and information-theoretic ideas that the more formal texts develop rigorously.

### 7. Stochastic Processes: The Mathematical Machinery

**S5--S6: Grimmett and Stirzaker, *Probability and Random Processes* (4th ed., 2020) and *One Thousand Exercises in Probability* (3rd ed., 2020)**

Grimmett and Stirzaker provide the comprehensive graduate-level treatment of probability and stochastic processes that supports the technical arguments throughout these notes. Where Kolmogorov establishes the foundations and Jaynes provides the interpretive framework, Grimmett and Stirzaker build the machinery: generating functions, branching processes, Markov chains (discrete and continuous time), renewal theory, queuing theory, martingales, and diffusions.

For the risk section, the relevant tools are laws of large numbers (which ground the almost-sure convergence claims of the Kelly criterion), random walk theory (which models sequential betting), martingale theory (which provides the stopping-time arguments behind gambler's ruin), and Brownian motion (which approximates the continuous-time limit of repeated wagering). For the information theory section, the asymptotic equipartition property and large deviation bounds connect to typical sequences and coding theorems.

The companion exercise book is essential for self-study. It is difficult to internalize probability and process intuition without working substantial problem sets. The exercises range from routine calculations to substantial proofs that develop technique in conditioning, generating functions, and martingale arguments.

A minor bibliographic note: the original webpage spells the authors' names as "Grimmet and Stirzacker." The correct spellings are Grimmett and Stirzaker.

---

## Part II: Information Theory

### 8. Overview: Information Beyond Communication

Shannon's 1948 paper "A Mathematical Theory of Communication" introduced entropy as a measure of information and established the fundamental limits of data compression and reliable communication. But information theory has grown well beyond its origins in communication engineering. It now encompasses algorithmic complexity (what is the information content of a single string?), information geometry (what is the natural geometric structure on spaces of probability distributions?), and the physics of information (what are the thermodynamic costs of computation?).

The information theory section of these notes surveys ten sources organized along these axes. The classical communication-theoretic line runs from Pierce's accessible introduction through Roman's algebraic coding theory, MacKay's unifying treatment of inference and learning, to Cover and Thomas's definitive graduate text. The algorithmic line is represented by Chaitin. The geometric line by Ciaglia et al. and Nielsen. The physical line by Bais and Farmer and by Wolpert. DeDeo provides an accessible on-ramp to the entire section.

### 9. Classical Information Theory: The Communication Perspective

**S7: Pierce, *An Introduction to Information Theory: Symbols, Signals and Noise* (1980; Dover reprint)**

Pierce's book is the gentlest entry point to Shannon's theory. Written by a Bell Labs scientist, it emphasizes conceptual clarity over formalism: entropy as a measure of uncertainty, channel capacity as the maximum rate of reliable communication, and coding as the art of matching source statistics to channel constraints. The treatment is qualitative where necessary and quantitative where it helps, making it suitable for technically literate readers who have not yet encountered the formal theory.

Within the present bibliography, Pierce serves as preparation for the more rigorous treatments that follow. It is the place to build intuition about why $H(X) = -\sum p(x_i) \log p(x_i)$ is the "right" measure of uncertainty before encountering the axiomatic derivation in Cover and Thomas.

**S9: Roman, *Coding and Information Theory* (1992)**

Roman's text occupies the algebraic wing of information theory: source coding (entropy, data compression), channel coding (error correction, capacity), and the algebraic structures (linear codes, cyclic codes, BCH and Reed-Solomon codes) that make reliable communication practically achievable. The mathematical treatment uses linear algebra and abstract algebra, making it accessible to readers with standard graduate-level algebra preparation.

This is the text to consult if one wants to understand codes as explicit constructions rather than existence theorems. The coding-theoretic perspective complements the probabilistic perspective in Cover and Thomas: the former asks "how do we build good codes?", the latter asks "what limits do the laws of probability impose?"

**S10: MacKay, *Information Theory, Inference and Learning Algorithms* (2003)**

MacKay's text is arguably the most aligned with the spirit of these notes: it treats information theory, Bayesian inference, and machine learning as one unified story. The through-line is that good probabilistic models compress data, and good codes can be understood via probabilistic inference. Shannon's source coding theorem says that the entropy $H(X)$ is the minimum average number of bits per symbol needed to represent a source; Bayesian model comparison asks which model compresses the data most efficiently, penalizing complexity through Occam factors.

The book covers entropy and mutual information, source and channel coding, error-correcting codes (including turbo codes and LDPC codes viewed through the lens of graphical models), Monte Carlo methods, neural networks, and Gaussian processes. It is freely available as a PDF from the author's website, which substantially lowers the barrier to entry.

MacKay's treatment sits between DeDeo (accessible but brief) and Cover and Thomas (comprehensive but formal). For a reader following the arc of these notes, it is the natural text to read after DeDeo's two primers and before tackling Cover and Thomas.

**S11: Cover and Thomas, *Elements of Information Theory* (2nd ed., 2005)**

This is the definitive graduate text. The treatment is rigorous and comprehensive: entropy, relative entropy (Kullback-Leibler divergence), mutual information, the data processing inequality, source coding, channel capacity, rate-distortion theory, Kolmogorov complexity, network information theory, and connections to statistics and hypothesis testing.

For the present notes, the most important results are the asymptotic equipartition property (which establishes typical sequences as the foundation of coding theory), the channel coding theorem (which gives the maximum rate of reliable communication), and the treatment of Kullback-Leibler divergence $D_{\mathrm{KL}}(p \| q) = \sum p(x) \log \frac{p(x)}{q(x)}$ as the fundamental measure of distributional discrepancy. The KL divergence reappears in the risk section through its connection to log-optimal betting: the Kelly criterion maximizes expected log wealth, which is equivalent to minimizing a KL-like quantity between the bettor's strategy and the growth-optimal strategy.

Cover and Thomas is also where one finds the formal treatment of Kolmogorov complexity that complements Chaitin's more idiosyncratic exposition (S8).

### 10. Algorithmic Information Theory

**S8: Chaitin, *Algorithmic Information Theory* (1987)**

Shannon entropy is a property of probability distributions---it measures average uncertainty. Algorithmic information theory, developed independently by Solomonoff, Kolmogorov, and Chaitin, asks a different question: what is the information content of a single string? The answer is the Kolmogorov complexity $K(x)$: the length of the shortest program that produces $x$ on a universal Turing machine.

A string is algorithmically random if no program shorter than the string itself can produce it -- that is, if 

$ K(x) \geq \mid x \mid $. 

This definition connects randomness to incompressibility: a random string cannot be compressed. The resulting theory has deep connections to Gödel's incompleteness theorems (there exist strings whose complexity cannot be proved to exceed any given bound) and to the halting problem (Kolmogorov complexity is uncomputable).

Chaitin's monograph develops these ideas with mathematical rigor; background in computability theory is assumed. The book introduces Chaitin's $\Omega$---the halting probability of a universal computer---which is a well-defined real number that is algorithmically random and contains, in a precise sense, the answers to all halting questions.

Placed alongside Shannon's distributional framework, algorithmic information theory provides the individual-sequence counterpart. The two perspectives are complementary: Shannon theory governs the average behavior of sources, while algorithmic theory governs the complexity of individual outputs. This complementarity is relevant to the physics-of-computation papers (S12, S15), where the thermodynamic cost of processing depends on both the input distribution and the specific computation being performed.

### 11. Information Geometry

**S13: Ciaglia, Di Cosmo, Felice, and Mancini, *Hamilton-Jacobi Approach to Potential Functions in Information Geometry* (arXiv:1608.06584, 2016)**

**S16: Nielsen, *The Many Faces of Information Geometry* (Notices of the AMS, 2022)**

Information geometry treats families of probability distributions as differential manifolds equipped with natural geometric structures. The Fisher information matrix $g_{ij}(\theta) = E\left[\frac{\partial \log p(x;\theta)}{\partial \theta_i} \frac{\partial \log p(x;\theta)}{\partial \theta_j}\right]$ provides a Riemannian metric that is invariant under sufficient statistics---a result due to Chentsov that characterizes the Fisher metric as essentially unique.

Nielsen's survey article provides a broad, readable introduction to the field. It covers the Fisher information metric, Amari's dual affine connections (the $\alpha$-connections that generalize the Levi-Civita connection), divergence functions as generating objects for the geometric structure, and applications spanning statistics, signal processing, and machine learning. For a reader with background in differential geometry, this article efficiently conveys the essential structures and their significance.

Ciaglia et al. develop a specific technical contribution: viewing potential (contrast) functions on statistical manifolds through the lens of Hamilton-Jacobi theory. They define a family of Lagrangians constructed from the metric tensor $g$ and the skewness tensor $T$ on a statistical manifold, and show that a complete solution of the associated Hamilton-Jacobi equation yields a potential function whose derivatives recover $g$ and $T$. This reinterpretation---"find a potential function" is equivalent to "solve a Hamilton-Jacobi problem"---connects information geometry to classical mechanics in a precise way.

For the physicist, this connection is suggestive. The Hamilton-Jacobi formalism is the gateway to quantum mechanics (through the WKB approximation) and to optimal control (through the Hamilton-Jacobi-Bellman equation). The information-geometric setting hints at dynamical formulations of statistical inference that parallel the dynamical formulations of physics. Whether this analogy can be made productive remains an active research question.

### 12. The Physics of Information

**S12: Bais and Farmer, *The Physics of Information* (arXiv:0708.2837, 2007)**

**S15: Wolpert, *Overview of Information Theory, Computer Science Theory, and Stochastic Thermodynamics for Thermodynamics of Computation* (arXiv:1901.00386, 2019)**

These two survey papers examine information from a physical perspective, connecting Shannon's mathematical framework to thermodynamics, computation, and the fundamental limits imposed by physics.

Bais and Farmer provide a broad survey spanning classical entropy (Boltzmann, Gibbs, Shannon), nonequilibrium thermodynamics, complexity, and quantum information. The paper's central argument is that information is not merely an abstract mathematical quantity but a physical one: it occupies space, requires energy to process, and obeys thermodynamic constraints. Landauer's principle---that erasing one bit of information dissipates at least $kT \ln 2$ of energy as heat---provides the concrete link between Shannon entropy and the second law of thermodynamics. The treatment extends to quantum information theory, covering qubits, entanglement, quantum entropy, no-cloning, and the basics of quantum computation.

Wolpert's chapter-length survey is more technically focused. Its central deliverable is an exact decomposition of entropy flow for a computational process:

$$\Sigma = \Sigma_{\mathrm{Landauer}} + \Sigma_{\mathrm{mismatch}} + \Sigma_{\mathrm{residual}}$$

where $\Sigma_{\mathrm{Landauer}}$ is the drop in Shannon entropy of the logical state (the "Landauer cost"), $\Sigma_{\mathrm{mismatch}}$ involves KL divergences between actual and counterfactual input distributions, and $\Sigma_{\mathrm{residual}}$ captures implementation-specific dissipation. This decomposition makes precise which thermodynamic costs depend only on the logical map and input distribution and which depend on the physical implementation.

The decomposition clarifies a longstanding confusion about reversible computation: reversibility eliminates the Landauer cost but not necessarily the mismatch or residual terms. The thermodynamic efficiency of computation thus depends on matching the physical implementation to the logical structure of the computation, not merely on making the computation logically reversible.

For the present notes, these papers serve two purposes. First, they legitimize "information" as more than communication theory---it is a physical quantity with thermodynamic consequences. Second, they demonstrate that the same Shannon/KL primitives introduced in the classical information theory texts (S10, S11, S14) have direct physical content, connecting the mathematical formalism to the natural world.

A bibliographic note: the original page labels Wolpert's paper as 2018. The arXiv identifier (1901.00386) and the PDF revision dates indicate 2019. This is a minor discrepancy.

### 13. Accessible Introductions to Information Theory

**S14: DeDeo, *Information Theory for Intelligent People* (2018)**

DeDeo's information theory notes form a natural pair with his Bayesian primer (S4). The document covers Shannon entropy and its axiomatic characterization (continuity, symmetry, maximum at the uniform distribution, the coarse-graining property), Huffman encoding as a constructive optimal coding scheme, KL divergence as a measure of "coding failure" or Bayesian surprise, mutual information, and Jensen-Shannon divergence as a proper metric on distributions.

Key formulas presented include:

- Shannon entropy: $H(X) = -\sum p(x_i) \log_2 p(x_i)$
- KL divergence: $D_{\mathrm{KL}}(q \| p) = \sum q(x_i) \log_2 \frac{q(x_i)}{p(x_i)}$
- Jensen-Shannon divergence: $\mathrm{JSD}(P, Q) = H(M) - \frac{1}{2}[H(P) + H(Q)]$ where $M = \frac{1}{2}(P + Q)$

The document's discussion of the Einstein/Cromwell rule---that assigning zero probability to any event creates the possibility of infinite surprise---is particularly relevant for Bayesian practitioners. It connects directly to the risk section: in sequential betting, assigning zero probability to an outcome that then occurs leads to total ruin.

DeDeo's notes are the best place to start before tackling Cover and Thomas. They build intuition for what information measures do and do not quantify without overwhelming the reader with theorem-proof formalism.

---

## Part III: Risk

### 14. Overview: From Games to Growth-Optimal Strategies

The risk section of these notes focuses on the mathematics of gambling and the Kelly criterion. This is a deliberate narrowing: "risk" in its broadest sense encompasses portfolio theory, insurance, decision theory, and much else. But the gambling context has several pedagogical advantages. The problems are concrete and well-defined. The relevant probability distributions are known (or can be estimated from data). The payoff structures are simple enough to admit closed-form solutions. And the historical development, centered on E. O. Thorp's work from the 1960s onward, provides a compelling narrative arc from pure mathematics to practical application.

The central mathematical object is the Kelly criterion. For a favorable binary bet with probability $p > 1/2$ of winning even money and probability $q = 1 - p$ of losing, the growth-optimal fraction of capital to wager is:

$$f^* = p - q = 2p - 1$$

For uneven payoffs (win $b$ for each unit wagered, lose 1), the optimal fraction generalizes to:

$$f^* = \frac{bp - q}{b}$$

The growth rate under Kelly betting is:

$$g(f) = p \log(1 + f) + q \log(1 - f)$$

which is maximized at $f = f^*$. The key insight---due to Kelly (1956), with asymptotic justification by Breiman (1961)---is that maximizing expected logarithmic wealth leads to almost-sure long-run dominance over any essentially different strategy.

This criterion is information-theoretic in origin. Kelly was Shannon's colleague at Bell Labs, and his criterion maximizes the rate of wealth growth, which is analogous to maximizing the rate of information transmission through a noisy channel. The connection is exact: the growth rate $g(f^*)$ equals the capacity of the "gambling channel" minus the entropy of the source of randomness.

The twelve sources in this section range from popular accounts (Thorp's *Beat the Dealer*) to rigorous probability treatments (Ethier) to the definitive edited research volume (MacLean, Thorp, and Ziemba). They are discussed roughly in order of increasing mathematical sophistication, with Thorp's contributions treated first as a coherent body of work.

### 15. Thorp: A Body of Work

**S17: Thorp, *Beat the Dealer* (1966)**
**S18: Thorp, *Kelly Money Management* (1979)**
**S19: Thorp, *The Mathematics of Gambling* (1984)**
**S20: Thorp, *The Kelly Criterion in Blackjack, Sports Betting, and the Stock Market* (1997)**
**S25: Thorp, *A Man for All Markets* (2017)**

Edward O. Thorp occupies a unique position in the intellectual landscape mapped by these notes: he is simultaneously a mathematician, a practitioner, and a popularizer. His work traces a progression from card counting (applied probability) through the Kelly criterion (information theory meets decision theory) to quantitative finance (continuous-time stochastic processes).

*Beat the Dealer* (S17) is the historical starting point. Published in 1966 (first edition 1962), it demonstrated that blackjack could be beaten by tracking the changing composition of the deck and adjusting bet sizes accordingly. The mathematical content---conditional expected values as a function of deck composition, basic strategy as an optimization over a Markov decision process---is embedded in a narrative of casino play that made the book a bestseller. Its significance for these notes is that it provided the first mass-market demonstration that probability theory could generate actionable edge in a real-world repeated game.

*Kelly Money Management* (S18) and *The Mathematics of Gambling* (S19) extend the analysis. The former is a short exposition of the Kelly criterion for practitioners; the latter surveys the mathematical structure of various casino games (blackjack, roulette, baccarat, craps, backgammon) and discusses the Kelly system in the context of each.

The technical centerpiece is S20: Thorp's comprehensive paper on the Kelly criterion. This document develops the theory with mathematical care and discusses both the theoretical properties and practical limitations of growth-optimal betting. The key results, established rigorously by Breiman (1961), are:

1. If $g(f) > 0$, wealth grows to infinity almost surely.
2. If $g(f) < 0$, wealth converges to zero almost surely.
3. If $g(f) = 0$, wealth oscillates between zero and infinity.
4. Kelly betting asymptotically dominates any "essentially different" strategy in the sense that the ratio of Kelly wealth to alternative wealth grows without bound.
5. Kelly betting minimizes the expected time to reach any specified wealth goal.

Thorp also develops practitioner-relevant formulas. The probability of ever being reduced to fraction $x$ of peak wealth is approximately $x^{2m/s^2}$, where $m$ and $s^2$ are the mean and variance of the per-bet log return. For full Kelly betting, this simplifies: the probability of ever halving is approximately 50%.

The continuous-time extension yields:

$$g_\infty(f) = r + f(m - r) - \frac{s^2 f^2}{2}$$

where $r$ is the risk-free rate, $m$ is the expected return, and $s^2$ is the variance. The optimal fraction becomes $f^* = (m - r)/s^2$, which is recognizable as the Sharpe ratio divided by volatility---a connection to modern portfolio theory.

Perhaps the most practically important result is the analysis of fractional Kelly. Half-Kelly betting achieves 75% of the full Kelly growth rate but substantially improves downside protection: the probability of doubling before halving rises from 2/3 (full Kelly) to 8/9 (half Kelly). This tradeoff between asymptotic optimality and finite-horizon risk management is a recurring theme in the risk literature.

*A Man for All Markets* (S25) is Thorp's memoir, providing narrative and historical context: how the blackjack work was done, how similar quantitative thinking entered finance through Princeton-Newport Partners, and how the first wearable computer was built to beat roulette. For readers using these notes for self-study, the memoir is not required mathematics, but it calibrates expectations about the human and institutional constraints around exploiting an edge.

### 16. The Kelly Criterion: Edited Research Volume

**S22: MacLean, Thorp, and Ziemba (eds.), *The Kelly Capital Growth Investment Criterion: Theory and Practice* (2011)**

This large edited volume attempts to be definitive on the Kelly capital growth criterion. It reprints key historical documents (Bernoulli on logarithmic utility, Kelly's original paper, Breiman's asymptotic theorems) and adds modern chapters on continuous-time finance, universal portfolios, the value of information in betting, and empirical investor behavior.

The volume makes explicit the practitioner tension at the heart of Kelly betting: full Kelly dominates asymptotically but can be psychologically and operationally difficult due to large drawdowns. Several chapters address this tension through fractional Kelly strategies, drawdown constraints, and risk-adjusted performance metrics.

For the information-theoretic thread of these notes, the volume is significant because it collects in one place the various formalisms connecting Kelly's criterion to Shannon's theory: the gambling channel, the information rate of wealth growth, and the minimax properties of log-optimal portfolios relative to KL divergence.

A bibliographic note: the original page spells the third editor's name as "Zeimba." The correct spelling is Ziemba.

### 17. Mathematics of Games and Gambling: Textbook Treatments

The remaining sources in the risk section provide textbook treatments of gambling mathematics at various levels of rigor and accessibility.

**S21: Packel, *The Mathematics of Games and Gambling* (2nd ed., 2006)**

An accessible MAA/AMS introduction requiring only high-school algebra. Packel develops probability, expectation, and elementary game theory through concrete examples from dice, cards, and casino games. This is the gentlest entry point to the risk section: it builds intuition about odds, expectation, and strategy before the reader encounters the more formal treatments.

**S23: Epstein, *The Theory of Gambling and Statistical Logic* (2nd ed., 2012)**

A broad, sometimes whimsical but mathematically serious tour of gambling, games, and statistical reasoning. Epstein treats gambling as a laboratory for probability, decision theory, and statistical logic. The coverage includes coins and wheels, dice, cards, blackjack, bridge, and even the question of whether statistical inference can evaluate paranormal claims. Later editions add material on computational competition and quantum games.

The book's distinctive feature is its breadth: it provides a broad alternative to the Kelly-centric path. Even without adopting the Kelly framework, one can learn a great deal about probabilistic reasoning and its pitfalls by analyzing gambling games.

**S24: Ethier, *The Doctrine of Chances: Probabilistic Aspects of Gambling* (2016)**

Ethier's text is the most rigorous "probability through gambling" treatment in this collection. It explicitly positions itself as a modern successor to de Moivre's 1718 classic of the same title, using gambling problems as a vehicle for deep probability theory: conditional expectation, martingales, Markov chains, Brownian motion, and stopping times.

The structure is telling: Part I develops the theory (probability review, conditional expectation, martingales, Markov chains, Brownian motion), and Part II applies it to gambling problems (house advantage, gambler's ruin, optimal play, and the Kelly criterion). This is the text to choose if one wants the full mathematical apparatus behind the topics, not merely the intuitions. The problem sets are substantial and appropriate for advanced graduate students.

Within the present bibliography, Ethier uses many of the tools developed in Grimmett and Stirzaker (S5) but channels them toward gambling and risk problems. It provides rigorous underpinning for the practical money-management discussions around Kelly.

**S26: Werthamer, *Risk and Reward: The Science of Casino Blackjack* (2nd ed., 2018)**

Werthamer's Springer monograph is distinctive in emphasizing not just optimal strategy but the distribution of outcomes and risk measures under realistic play conditions. The associated interactive figures (hosted via Wolfram Cloud) illustrate how risk of ruin, effective yield, and performance metrics vary as functions of strategy parameters and bankroll size.

The book's core message reinforces a theme that runs through the entire risk section: expected value is only part of the story. Risk metrics and capital constraints shape the real decision problem. Kelly optimizes asymptotic growth; Werthamer foregrounds finite-horizon risk and outcome distributions.

**S27: Bewersdorff, *Luck, Logic, and White Lies: The Mathematics of Games* (2nd ed., 2021)**

A broad tour of the mathematics of games of chance and strategy, designed to be readable and example-driven. Bewersdorff uses a "game fragment followed by mathematical tool" pedagogical loop, bringing in probability, combinatorics, and strategic reasoning as needed. Compared to Packel, it ranges more widely into strategic games and game-theoretic ideas.

**S28: Bollman, *Basic Gambling Mathematics: The Numbers Behind the Neon* (2nd ed., 2023)**

An introductory probability textbook organized around gambling contexts: counting, distributions, expectation, and house advantage using real casino and betting examples. The treatment is systematic, with a clear progression and exercises. For a reader whose end goal is the risk and finance material, this provides a "practical probability" track grounded in concrete numerical calculation.

---

## 18. Synthesis: How the Three Threads Connect

### The Entropy Thread

The deepest connection across these three sections is entropy. Shannon entropy $H(X)$ appears first in Part I as a consequence of Jaynes's maximum entropy principle (the canonical distribution maximizes entropy subject to energy constraints). It appears in Part II as the fundamental quantity in coding theory (the source coding theorem), as the basis for channel capacity ($C = \max_{p(x)} I(X;Y)$), and as a physical quantity with thermodynamic content (Landauer's principle). It appears in Part III as the objective function for growth-optimal betting (Kelly's criterion maximizes the expected growth rate, which equals $H(X) - H(X \mid Y)$ for the gambling channel, i.e., the mutual information between the gambler's side information and the game outcome).

This is not coincidence. All three appearances reflect the same underlying mathematical structure: the logarithmic function connects multiplicative processes (compounding of wealth, nesting of codes, multiplication of Boltzmann weights) to additive quantities (growth rates, code lengths, energies). Entropy is the expected value of the negative logarithm of probability, and this particular functional form is singled out by axiomatic arguments (Shannon, Khinchin), by consistency requirements (Cox, Jaynes), and by asymptotic optimality (Kelly, Breiman).

### The KL Divergence Thread

Kullback-Leibler divergence $D_{\mathrm{KL}}(p \| q)$ provides a second unifying thread. In information theory, it measures the excess coding cost of using code $q$ when the true distribution is $p$. In Bayesian inference, the expected KL divergence from prior to posterior measures the information gained from an experiment. In the physics of computation, KL divergences appear in the mismatch cost of Wolpert's entropy-flow decomposition. In risk management, sub-optimal betting (using fraction $f \neq f^*$) incurs a growth-rate penalty that can be expressed as a KL-like quantity.

### Three Learning Paths

The bibliography supports at least three coherent self-study curricula, depending on the reader's goals and background:

**Foundations track (rigor-first):** Kolmogorov (S1) establishes the measure-theoretic framework. Grimmett and Stirzaker (S5, S6) build the stochastic process machinery. Cover and Thomas (S11) formalize information measures. Ethier (S24) applies rigorous probability to gambling. MacLean, Thorp, and Ziemba (S22) provide the research-level Kelly treatment.

**Inference track (Bayes-first):** Jaynes (S2) provides the philosophical foundation. DeDeo (S4, S14) makes Bayesian reasoning and information theory operational. Mumford and Desolneux (S3) demonstrate Bayesian modeling on structured spaces. MacKay (S10) unifies inference, coding, and learning. Thorp (S20) connects inference to sequential decision-making.

**Physics/geometry track (information as structure):** Bais and Farmer (S12) survey information as a physical quantity. Wolpert (S15) decomposes the thermodynamic costs of computation. Nielsen (S16) introduces information geometry. Ciaglia et al. (S13) develop Hamilton-Jacobi methods on statistical manifolds.

### Gaps and Natural Extensions

These notes, like the original bibliography, are deliberately selective. Several natural extensions suggest themselves but are not yet developed:

*Decision theory and utility beyond logarithmic utility.* The Kelly criterion implicitly assumes logarithmic utility. Alternative utility functions (CARA, CRRA, prospect theory) lead to different optimal strategies. The relationship between Kelly betting and expected utility maximization is well-studied but not surveyed here. Instead it appears in later chapters. 

*Risk measures and portfolio constraints.* The Kelly framework assumes unlimited access to capital and no leverage constraints. Real portfolio management involves drawdown constraints, value-at-risk (VaR), conditional value-at-risk (CVaR), and regime uncertainty. These topics connect to convex optimization and robust control as described in subsequent chapters.

*Stochastic calculus and continuous-time finance.* Thorp's continuous-time Kelly formula hints at the Black-Scholes-Merton framework and the theory of continuous-time portfolio optimization (Merton's problem). These connections are developed in the broader *Projects in Scientific Computing* collection under stochastic calculus.

*Machine learning optimization.* The connections between information-theoretic objectives (cross-entropy loss, KL regularization, mutual information maximization) and modern machine learning training procedures are substantial and considered in and of themselves in the machine learning chapter.

---

## Bibliography

### Probability

| ID  | Link | Notes |
|-----|------|-------|
| S1  | [Kolmogorov *"Foundations of Probability"* 1956](https://www.york.ac.uk/depts/maths/histstat/kolmogorov_foundations.pdf) | Seminal work laying the axiomatic foundations of modern probability theory. |
| S2  | [Jaynes *"Probability: The Logic of Science"* 2003](https://sites.astro.caltech.edu/~george/ay122/Jaynes-book.pdf) | A Bayesian reinterpretation of probability as logic extended to uncertain reasoning. |
| S3  | [Mumford and Desolneux *"Pattern Theory"* 2010](https://www.dam.brown.edu/ptg/MDbook/index.html) | Explores probabilistic models of perception, inference, and structure in complex systems. |
| S4  | [DeDeo *"Bayes for Intelligent People"* 2018](https://wiki.santafe.edu/images/2/2e/Bayesian-Reasoning-for-Intelligent-People-DeDeo.pdf) | Introductory guide to Bayesian reasoning and inference for advanced learners. |
| S5  | [Grimmet and Stirzacker *"Probability and Random Processes"* 2020](https://global.oup.com/academic/product/probability-and-random-processes-9780198847601?cc=us&lang=en&) | Comprehensive textbook on probability and stochastic processes. |
| S6  | [Grimmet and Stirzacker *"One Thousand Exercises in Probability"* 2020](https://global.oup.com/academic/product/one-thousand-exercises-in-probability-9780198847618?cc=us&lang=en&) | Problem book accompanying the main text on probability and random processes. |

### Information Theory

| ID  | Link | Notes |
|-----|------|-------|
| S7  | [Pierce *"Introduction to Information Theory"* 1980](https://store.doverpublications.com/products/9780486240619?srsltid=AfmBOopmY5Ja4x4dTGxhin4FAuJPd-fPtNj78zgLiwZW9CUdD7TyvRvq) | Classic introduction to the principles and applications of information theory. |
| S8  | [Chaitin *"Algorithmic Information Theory"* 1987](https://www.cambridge.org/core/books/algorithmic-information-theory/66D88D412DE158C21D392E2EF3112CC1#fndtn-information) | Explores complexity and randomness through the lens of algorithmic information. |
| S9  | [Roman *"Coding and Information Theory"* 1992](https://link.springer.com/book/9780387978123) | Textbook covering the fundamentals of coding theory and information transmission. |
| S10 | [MacKay *"Information Theory, Inference and Learning Algorithms"* 2003](https://www.cambridge.org/us/universitypress/subjects/computer-science/pattern-recognition-and-machine-learning/information-theory-inference-and-learning-algorithms?format=HB&isbn=9780521642989) | Comprehensive work connecting information theory with inference and learning. |
| S11 | [Cover and Thomas *"Elements of Information Theory"* 2005](https://onlinelibrary.wiley.com/doi/book/10.1002/047174882X) | Definitive textbook on the mathematical foundations of information theory. |
| S12 | [Bais and Farmer *"The Physics of Information"* 2007](https://arxiv.org/abs/0708.2837) | Investigates information theory from a physical and thermodynamic perspective. |
| S13 | [Ciaglia et al *"HJ Approach to Potential Functions in Information Geometry"* 2016](https://arxiv.org/abs/1608.06584) | Presents a Hamilton-Jacobi framework for potential functions in information geometry. |
| S14 | [DeDeo *"Information Theory for Intelligent People"* 2018](https://wiki.santafe.edu/images/a/a8/IT-for-Intelligent-People-DeDeo.pdf) | Accessible introduction to key ideas in information theory for thoughtful readers. |
| S15 | [Wolpert *"Information Theory, Computer Science, Stochastic Thermodynamics"* 2018](https://arxiv.org/abs/1901.00386) | Interdisciplinary exploration of the intersections between information theory and physics. |
| S16 | [Nielsen *"Information Geometry"* 2022](https://www.ams.org/notices/202201/rnoti-p36.pdf) | Review of key concepts and applications in the geometry of statistical models. |

### Risk

| ID  | Link | Notes |
|-----|------|-------|
| S17 | [Thorp *"Beat The Dealer"* 1966](https://www.edwardothorp.com/books/beat-the-dealer/) | Pioneering book on card counting strategies in blackjack. |
| S18 | [Thorp *"Kelly Money Management"* 1979](https://www.edwardothorp.com/wp-content/uploads/2016/11/TheKellyMoneyManagementSystem.pdf) | Explains the Kelly criterion for optimal bet sizing in gambling and investing. |
| S19 | [Thorp *"The Mathematics of Gambling"* 1984](https://www.edwardothorp.com/books/the-mathematics-of-gambling/) | Mathematical principles underlying various gambling games. |
| S20 | [Thorp *"Kelly Criterion"* 1997](https://web.williams.edu/Mathematics/sjmiller/public_html/341/handouts/Thorpe_KellyCriterion2007.pdf) | Discussion on the theory and application of the Kelly strategy. |
| S21 | [Packel *"The Mathematics of Games and Gambling"* 2006](https://www.ams.org/books/nml/028/nml028-endmatter.pdf) | A mathematical exploration of gambling and game theory. |
| S22 | [Maclean, Thorp, and Zeimba *"Kelly Capital Growth Investment Criterion"* 2011](https://www.edwardothorp.com/books/kelly-capital-growth-investment-criterion/) | Advanced treatments of the Kelly criterion in investment and gambling contexts. |
| S23 | [Epstein *"Theory of Gambling and Statistical Logic"* 2012](https://shop.elsevier.com/books/the-theory-of-gambling-and-statistical-logic/epstein/978-0-12-397857-8) | Comprehensive mathematical treatment of gambling and probability. |
| S24 | [Ethier *"Doctrine of Chances: Probabilistic Aspects of Gambling"* 2016](https://www.math.utah.edu/~ethier/DoC.html) | Rigorous study of the probability theory behind gambling. |
| S25 | [Thorp *"A Man for All Markets"* 2017](https://www.edwardothorp.com/books/a-man-for-all-markets/) | Thorp's memoir blending personal stories with his pioneering work in mathematics, gambling, and quantitative finance. |
| S26 | [Werthamer *"Risk and Reward: The Science of Casino Blackjack"* 2018](https://link.springer.com/book/10.1007/978-3-319-91385-8) | Scientific approach to strategy and probability in blackjack. |
| S27 | [Bewersdorff *"Luck, Logic, and White Lies: The Mathematics of Games"* 2021](https://www.taylorfrancis.com/books/edit/10.1201/9781003092872/luck-logic-white-lies-jörg-bewersdorff) | Explores the mathematics behind games, chance, and strategy. |
| S28 | [Bollman *"Basic Gambling Mathematics"* 2023](https://www.taylorfrancis.com/books/mono/10.1201/9781003358183/basic-gambling-mathematics-mark-bollman) | Introductory textbook on the fundamental math of gambling. |
