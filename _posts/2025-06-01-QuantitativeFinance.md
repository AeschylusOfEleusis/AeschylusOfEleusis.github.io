---
layout:   post
title: "Quantitative Finance"
date: 2025-06-01 10:00:00 +0800
categories: [Computational Finance]
tags: [Probability Information Risk, Quantitative Finance, Path Integrals, Stochastic Calculus, Computational Finance]
math:       true        # enable KaTeX
---
# Notes on Quantitative Finance (Draft)

## Abstract

These notes survey the literature of quantitative finance from the perspective of statistical physics, complexity science, and applied mathematics. The emphasis is on empirical stylized facts—fat-tailed return distributions, volatility clustering, long-memory in order flow, scaling properties—that emerge from statistical analysis of financial, economic, and social data, and that constrain the space of admissible theoretical models. The notes trace the intellectual migration of methods from physics to finance, beginning with chaos-theoretic time series analysis in the late 1980s and proceeding through econophysics, market microstructure, asset pricing, portfolio theory, risk management, and complexity economics. For completeness, the orthodox neoclassical treatment of asset pricing and portfolio theory is included alongside the physics-informed alternatives. Some history of the field is provided, including the influence over time of computation, applied mathematics, and theoretical physics—particularly the post–Cold War migration of physicists into financial engineering. The bibliography of approximately seventy sources, spanning four decades of research (1987–2024), is organized into seven thematic sections that progress from data and measurement through theoretical frameworks to applications and synthesis. Suggested learning paths and identification of gaps in coverage are provided throughout.

---

## 1. Introduction

Quantitative finance sits at an intersection of several intellectual traditions that do not always communicate well with one another. Orthodox financial economics, rooted in neoclassical equilibrium theory, proceeds from axioms about rational agents and derives consequences for asset prices, risk premia, and portfolio allocation. Statistical physics, by contrast, begins with empirical measurement—distributions, correlations, scaling exponents—and builds theoretical models constrained by what the data actually show. Between these poles lies a third tradition, complexity economics, which models markets as adaptive systems of interacting heterogeneous agents, drawing on evolutionary dynamics, network theory, and agent-based computation.

The literature surveyed here reflects all three traditions, though the center of gravity is unmistakably the physics-informed approach. This is a deliberate choice. The standard finance curriculum is well served by excellent textbooks (Cochrane, Duffie, Campbell–Lo–MacKinlay) that are included here primarily as reference points. What these notes add is a systematic guide to the econophysics literature—the body of work that takes seriously the empirical departures from Gaussian assumptions, that applies random matrix theory to covariance estimation, that models limit order books as stochastic partial differential equations, and that treats market crashes as critical phenomena rather than exogenous shocks.

The organization follows the structure of the subject. Sections 2 through 4 address data: the methods for analyzing financial time series, the empirical regularities ("stylized facts") that any adequate model must reproduce, and the mechanics of price formation at the transaction level. Sections 5 and 6 treat theory: asset pricing frameworks (both orthodox and physics-informed) and portfolio construction with factor analysis. Section 7 covers risk measurement and management, where the practical consequences of getting the distributional assumptions wrong are most acute. Section 8 concludes with complexity economics, the broadest theoretical framework within which the preceding topics can be situated. A final section identifies cross-cutting themes and structural relationships among the sources.

A note on the bibliography: approximately seventy sources are referenced, spanning journal articles, ArXiv preprints, monographs from Cambridge, Princeton, Springer, and other academic publishers, and a small number of practitioner-oriented texts. ArXiv preprints are included both for accessibility (many journal articles remain behind paywalls) and because significant work in econophysics circulates primarily through the preprint server. Where paywalled publisher links are the only option, this is noted. The source numbering (S1 through S70) follows the annotated bibliography on the companion webpage and is retained here for cross-referencing convenience.

---

## 2. Data: Time Series Analysis

The analysis of financial time series is the empirical foundation on which everything else rests. The literature collected in this section spans from pioneering chaos-theory applications in the late 1980s to contemporary machine learning approaches, and it exhibits a productive tension between two paradigms that has shaped the field for decades.

### 2.1 Two paradigms

The first paradigm is deterministic nonlinear dynamics. Farmer and Sidorowich (S1, 1987), publishing in *Physical Review Letters*, introduced phase-space reconstruction techniques for short-horizon forecasting of chaotic dynamics. Their method embeds scalar time series into higher-dimensional phase spaces using delay coordinates, enabling local linear prediction. This represented an early and ambitious attempt to apply dynamical systems theory to financial data—the hypothesis being that apparent randomness in price movements might conceal low-dimensional deterministic structure recoverable through appropriate embedding. Farmer's subsequent work on nonlinearity in time series (S2, 1992) pursued this line further, presenting evidence for low-dimensional deterministic structures in financial data.

The second paradigm is stochastic econometrics, which treats returns as fundamentally random processes to be characterized by their statistical properties. Hamilton's *Time Series Analysis* (S3, 1994) is the standard graduate reference here, covering ARIMA models, state-space representations, spectral analysis, and unit root tests. Campbell, Lo, and MacKinlay's *The Econometrics of Financial Markets* (S4, 1997) formalizes spectral tests, long-memory diagnostics, and GMM baselines for empirical factor models, establishing standards for empirical asset pricing research that remain current. Cochrane's lecture notes on time series for macroeconomics and finance (S5, 1997) connect discrete-time VAR/GMM estimation with continuous-time pricing kernels, providing the bridge from time series econometrics to asset pricing theory proper.

The tension between these paradigms is not merely academic. If financial time series contain exploitable deterministic structure, then prediction is in principle possible through phase-space methods. If returns are fundamentally stochastic, then the appropriate tools are statistical characterization and probabilistic forecasting. The resolution—or rather, the productive coexistence—of these views has shaped much of the subsequent literature.

### 2.2 Diagnostics before forecasting

A crucial intermediate step, well represented in the bibliography, is the development of diagnostic tools that can distinguish deterministic chaos from stochastic processes in empirical data. Kantz and Schreiber's *Nonlinear Time Series Analysis* (S6, 2004) details surrogate-data tests for detecting nonlinearity, correlation dimension estimation, and Lyapunov exponent calculation. These techniques provide the machinery for testing the chaos hypothesis rigorously rather than assuming it. Bradley and Kantz (S8, 2015) provide historical context for nonlinear time series analysis in an ArXiv review, tracing developments from Takens' embedding theorem through practical implementations and clarifying how modern practice differs from the early enthusiasm of the 1980s and 1990s. The verdict, broadly, is that robust evidence for low-dimensional chaos in financial data has been elusive—but that nonlinear dynamics remains a productive framework for understanding certain features of financial time series, particularly when combined with stochastic elements.

### 2.3 Machine learning as a third way

More recent sources gesture toward machine learning as an alternative function approximator that sidesteps the deterministic-vs-stochastic debate. Adhikari and Agrawal (S7, 2013) survey classical stochastic models alongside early neural networks and support vector machines for time-series forecasting, providing a useful map of model families. Ekapure et al. (S12, 2021) apply feature engineering and ML classifiers to short-horizon trend prediction in equity data—best read as an applied template rather than state-of-the-art methodology. Ruey and Chen (S10, 2019) survey methods for approaching nonlinearity more broadly. Marcaccioli and Livan (S11, 2019) take an intriguing path, mapping time-series inverse problems onto the spherical model from statistical mechanics, giving a physics-style interpretation of correlation constraints that bridges the two paradigms in a novel way.

### 2.4 Suggested learning path

For self-study, the natural starting point is Campbell–Lo–MacKinlay (S4) or Hamilton (S3) for core econometric grounding, read in parallel with Kantz and Schreiber (S6) for nonlinear diagnostics. Farmer and Sidorowich (S1, S2) provide the chaos/state-space reconstruction lineage and context for why it matters (or fails to matter) for finance. The survey papers (S7, S8, S10) map the broader method landscape. Cochrane's notes (S5) then connect time-series estimation to the pricing-kernel and factor-model objects that appear in later sections.

### 2.5 Gaps in the literature

Modern volatility modeling—ARCH/GARCH, realized volatility, stochastic volatility estimation—is not explicitly represented in this section, though elements appear elsewhere in the bibliography. Contemporary deep learning for financial time series (representation learning, transformers, probabilistic forecasting) is barely covered. These are deliberate omissions reflecting the physics-informed emphasis of the collection rather than oversights, but the reader should be aware that a parallel and rapidly growing literature exists in both areas.

---

## 3. Data: Empirical Stylized Facts

This is the most extensively developed section of the bibliography, with sixteen sources documenting the emergence and maturation of econophysics as a distinct intellectual enterprise. The central claim of econophysics is that financial data exhibit robust empirical regularities—"stylized facts"—that are poorly captured by the Gaussian assumptions of orthodox finance but naturally accommodated by methods from statistical physics. These stylized facts serve as empirical constraints on any admissible theoretical model.

### 3.1 Foundations

Mantegna and Stanley's *Introduction to Econophysics* (S14, 2000) is the foundational textbook, cited over a thousand times, and remains the natural entry point. It covers the efficient market hypothesis and its critique, random walks and Lévy processes, scaling properties of financial data, ARCH/GARCH processes, turbulence analogies, correlation structures, and options pricing—all viewed through the lens of statistical physics. The text systematically documents departures from Gaussian assumptions using empirical evidence from various markets.

Mandelbrot's *The Misbehavior of Markets* (S15, 2004) is the accessible synthesis of his decades-long critique of efficient market theory, tracing ideas from his seminal 1963 analysis of cotton prices through subsequent developments in multifractal analysis. Mandelbrot's argument for fractal scaling and α-stable processes over Gaussian models is historically important: it was Mandelbrot who first demonstrated, in the early 1960s, that the tails of return distributions are too heavy for the normal distribution, and this observation has never been satisfactorily incorporated into mainstream financial economics.

### 3.2 The econophysics reviews

The bibliography includes a substantial cluster of review papers (S17 through S26) that document the field's evolution from different angles. These are not redundant—they emphasize different aspects and reflect different moments in the field's development—but navigating among them requires some guidance.

Yakovenko (S17, 2008) reviews kinetic-exchange and related models for money, wealth, and income distributions, emphasizing Boltzmann–Gibbs intuition, conservation laws, and inequality measures. This is the statistical mechanics of wealth distribution rather than of asset prices per se. Chakraborti et al. (S18, 2010) provide the broadest single review, spanning stylized facts, order book statistics, correlation analysis (including random matrix theory and graph methods), and agent-based modeling of order-driven markets, wealth exchange, and minority games. This is probably the most useful survey for a reader wanting comprehensive coverage in a single source. Sornette (S21, 2014) provides a historical narrative tying economic puzzles to physics metaphors—Ising models, interacting agents—and arguing for agent-based models and out-of-equilibrium thinking. Bouchaud (S25, 2019) offers a candid perspective on what econophysics got right, where it failed to integrate with mainstream economics, and which problems are ripe for progress (microstructure, networks, agent-based models). This last review is particularly valuable for its intellectual honesty about the field's limitations.

Schinckus (S23, 2018) deserves special mention as a Cambridge PhD dissertation providing comprehensive history and philosophy-of-science analysis of econophysics. He identifies three methodological strands—statistical econophysics, bottom-up agent-based approaches, and top-down agent-based approaches—and argues that the field operates through empirically adequate analogies in the manner of Pierre Duhem. The Santa Fe Institute's complexity research program is identified as crucial to shaping the field's methodology, a theme that recurs in the final section on complexity economics.

Farmer et al. (S16, 2005), writing in *Physics Today*, advocate for the application of physicists' universality concepts to financial innovation—a programmatic statement that reads differently twenty years on, after the 2008 crisis demonstrated both the power and the limitations of quantitative methods in finance.

### 3.3 Random matrix theory

Two sources address random matrix theory (RMT), which provides a principled framework for separating signal from noise in the estimation of large covariance matrices—a problem of direct practical importance for portfolio construction.

Di Francesco, Ginsparg, and Zinn-Justin (S13, 1994) is a foundational review of random matrix theory in the context of 2D gravity and quantum field theory. It is not finance-specific, but it provides the mathematical infrastructure—eigenvalue distributions, universality classes, large-N limits—that underpins all subsequent applications of RMT to financial data. Potters and Bouchaud's *A First Course in Random Matrix Theory* (S27, 2020) is the finance-facing treatment, covering the Marčenko-Pastur distribution, eigenvalue cleaning techniques, and explicit applications to financial covariance estimation. For a reader approaching this material from physics, S13 provides the theoretical depth; for one approaching from finance, S27 is the practical starting point.

### 3.4 Multifractals and spin glasses

The more advanced material in this section pushes into territory that remains actively researched. Jiang, Xie, Zhou, and Sornette (S24, 2018) provide a 145-page review of multifractal analysis methods (MF-DFA, wavelets, partition functions), evidence for multifractality in financial data, sources of multifractality (fat tails versus long-range correlations), and applications to market inefficiency and risk assessment. This extends beyond simple power-law scaling to characterize the full spectrum of scaling exponents—a richer description of the data than any single-exponent model provides.

Bouchaud, Marsili, and Nadal (S28, 2023) apply spin-glass concepts—energy landscapes, replica symmetry breaking, the cavity method, marginal stability—to complex socio-economic data. This represents the frontier of physics methodology in finance, importing some of the deepest mathematical machinery from disordered systems theory. The conceptual payoff is a framework for thinking about multi-equilibria, fragility, and inference problems in systems with frustrated interactions—a description that fits financial markets uncomfortably well.

### 3.5 Suggested learning path

Begin with Mantegna and Stanley (S14) for a coherent entry point, then use Chakraborti et al. (S18) as the broadest single review. Dive into the multifractal review (S24) for multi-scale volatility structure. Use Potters and Bouchaud (S27) for finance-facing RMT, with Di Francesco et al. (S13) as deeper theoretical background. Read Bouchaud's perspective piece (S25) after the above for a candid assessment of the field's status.

---

## 4. Data: Market Microstructure

Where the previous section characterizes markets at the level of daily or lower-frequency returns, this section moves to the mechanics of price formation at the transaction level. The seven sources here span from early market ecology models (1996–1998) to contemporary SPDE approaches (2020), and they constitute the most "mechanistic" material in the collection—the section closest to a physical theory of how prices actually form.

### 4.1 Market impact and execution

Farmer's early work on slippage (S29, 1996) introduces market-impact cost functions, establishing foundational concepts for understanding how order flow affects prices. Market impact—the fact that buying pushes prices up and selling pushes them down, by amounts that depend on order size, market conditions, and execution strategy—is a first-order practical concern for anyone trading in size and a first-order theoretical challenge for anyone modeling price formation. The empirical regularity here is the square-root law of market impact: the price impact of a meta-order scales roughly as the square root of its size relative to daily volume. This is one of the most robust stylized facts in microstructure, and its theoretical explanation remains an active area of research.

### 4.2 Markets as complex adaptive systems

Farmer's *Market Ecology and Evolution* (S30, 1998) models trader populations using Lotka-Volterra dynamics to explain clustered volatility and intraday skew shifts. This ecological perspective—treating markets as ecosystems of interacting heterogeneous agents rather than as equilibria of identical rational agents—is conceptually rich and connects naturally to the complexity economics framework in Section 8. It also provides a mechanism (the interaction of different trading strategies) for generating empirical regularities (volatility clustering, fat tails) that orthodox models must impose by assumption.

Pompian (S31, 2006) catalogues cognitive biases from behavioral finance—a distinct tradition from physics-based approaches but one that addresses the same underlying question of why markets deviate from efficient-market predictions. The biases documented here (overconfidence, loss aversion, herding) can be understood as the micro-level substrate of the ecological dynamics that Farmer models at the population level.

### 4.3 Limit order books

The most substantial microstructure texts in the collection are Abergel's *Limit Order Books* (S32, 2016) and Bouchaud et al.'s *Trades, Quotes and Prices* (S34, 2018). Abergel documents empirical order-book stylized facts and develops agent-based models of limit order book dynamics—essential reading for understanding modern electronic market structure. Bouchaud et al. provide the comprehensive Cambridge treatment, covering limit order book mechanics, time clustering via Hawkes processes, long-range persistence of order flow, the square-root law of market impact, propagator models, and market-making profitability. This text is widely regarded as the definitive physics-informed treatment of market microstructure, combining quantitative rigor with practical trading insights.

Lehalle and Laruelle (S33, 2018) calibrate market impact, study order-flow clustering, and address liquidity and regulation from a more applied perspective. Cont and Mueller (S35, 2020) introduce stochastic partial differential equation modeling of limit order book dynamics, representing the mathematical frontier of continuous-time market microstructure theory. The SPDE approach is conceptually attractive because it provides a principled continuous-time limit of the inherently discrete order book—analogous to how fluid dynamics emerges from molecular dynamics—but the practical utility of these models for trading applications remains to be fully established.

### 4.4 Suggested learning path

Start with Farmer (S29) for the practical measurement of execution cost and impact. Read Bouchaud et al. (S34) or Abergel (S32) for empirical LOB facts and microstructure mechanisms, then Cont and Mueller (S35) for the formal continuous-time theory. Treat Farmer (S30) as conceptual enrichment—the ecology/evolution lens—rather than as a direct trading model.

### 4.5 Gaps in the literature

High-frequency market making and optimal execution research (inventory-based models, adverse selection) is not directly represented. Empirical market microstructure econometrics (Hawkes process estimation, message-level data pipelines) is only lightly covered. These are areas where significant recent progress has been made, particularly as electronic markets have become the dominant venue for price discovery.

---

## 5. Asset Pricing Theory

This section provides what might be called the "minimal orthodox core" of asset pricing theory alongside physics-inspired alternatives for risk and derivative pricing under non-Gaussian return laws. The structure reflects the bibliography's overall philosophy: include the standard references that any quantitative finance practitioner must know, then develop the alternatives that the stylized facts demand.

### 5.1 The orthodox spine

Cochrane's *Asset Pricing* (S37, 2000) derives the stochastic discount factor (SDF) framework central to modern asset pricing theory. The SDF approach unifies the capital asset pricing model, the arbitrage pricing theory, and various consumption-based models within a single mathematical framework: the price of any asset equals the expected value of its payoffs weighted by the SDF. This is the theoretical foundation for risk-neutral valuation and, by extension, for derivative pricing. It is also the framework within which the empirical anomalies—the equity premium puzzle, the risk-free rate puzzle, momentum, value—are most precisely stated.

Duffie's *Dynamic Asset Pricing Theory* (S38, 2001) provides rigorous Itô-calculus foundations for optimal exercise boundaries and contingent claim valuation in continuous time. Where Cochrane emphasizes the economic intuition and discrete-time foundations, Duffie provides the mathematical machinery of continuous-time finance that underlies the Black-Scholes framework and its extensions.

Tracy (S36, 1999) serves a different function: distilling accounting statements into cash-flow and leverage signals that can be engineered as factors. This is the unglamorous but necessary work of connecting theoretical asset pricing to observable financial data.

### 5.2 The physics-informed alternative

Bouchaud and Potters' *Theory of Financial Risk and Derivative Pricing* (S39, 2003) integrates heavy-tailed return statistics into Black-Scholes-type PDEs via fractional diffusions. This Cambridge text provides the theoretical bridge between observed fat-tailed distributions and derivative pricing frameworks—the attempt to take the stylized facts documented in Section 3 seriously within a pricing theory. The practical challenge is that abandoning the Gaussian assumption also abandons much of the analytical tractability that makes the Black-Scholes framework so useful, and the tradeoff between realism and tractability is a recurring theme in this literature.

Voit's *Statistical Mechanics of Financial Markets* (S40, 2005) applies statistical mechanical methods broadly to quantitative finance, providing additional context for the physics-informed approach. Kleinert (S41, 2016) takes the alternative framework to a specific application: option pricing when returns follow asymmetric α-stable Lévy laws, with analytic tractability achieved through regularization techniques. This addresses the concrete challenge of pricing derivatives under non-Gaussian assumptions—not merely documenting that returns are non-Gaussian (which is well established) but building pricing tools that accommodate this fact.

### 5.3 Suggested learning path

For mainstream finance theory, start with Cochrane (S37) then Duffie (S38). For non-Gaussian derivatives and risk, pair Bouchaud and Potters (S39) with Kleinert (S41), using Voit (S40) as broader context. Tracy (S36) is useful applied background for building factor signals from fundamentals.

### 5.4 Gaps in the literature

No explicit term-structure or fixed-income asset pricing text appears here, though Rebonato's yield-curve modeling (S48) appears in the next section. Derivatives coverage is selective, reflecting the non-Gaussian focus; volatility-surface modeling, local and stochastic volatility models, and numerical methods for derivative pricing are not explicitly treated. The reader needing a comprehensive derivatives curriculum should supplement with standard references (Hull, Shreve, Gatheral).

---

## 6. Multi-Asset Structures and Factor Analysis

This section addresses the problem of how assets relate to one another—through covariance structures, factor models, network representations, and portfolio optimization. The material ranges from classical mean-variance optimization through stress testing and Bayesian networks to unsupervised learning of market sectors and financial network analysis.

### 6.1 Portfolio theory: classical and beyond

The neoclassical starting point is Markowitz mean-variance optimization, presented rigorously in Joshi's *Mathematical Portfolio Theory* (S45, 2013) and extended to practical constraints in Prigent's *Portfolio Optimization* (S42, 2007), which includes quadratic programming routines for mean-variance allocation with option and transaction-cost constraints. Bodie, Kane, and Marcus (S49, 2018) provide the standard textbook treatment including CAPM and APT, while Brealey, Myers, and Allen (S50, 2019) cover corporate finance foundations.

The more interesting material, from the physics perspective, begins with Peters (S43, 2010), whose ergodicity economics program challenges expected utility theory by distinguishing time-average from ensemble-average returns. The argument is that the standard framework of expected utility maximization assumes ergodicity—that the time average of a quantity equals its ensemble average—and that this assumption fails for multiplicative processes like investment returns. The practical consequence is a justification for growth-optimal (Kelly) position sizing and leverage control that differs from the conventional mean-variance prescription. This is a foundational critique that, if correct, has implications across the entire field.

### 6.2 Stress testing and Bayesian methods

Rebonato and Denev (S46, 2013) apply Bayesian networks to asset allocation under stress, providing a principled framework for incorporating expert judgment about scenario dependencies into portfolio construction. Rebonato's yield-curve modeling text (S48, 2018) presents PCA-driven term-structure dynamics—the standard dimensionality reduction for fixed-income portfolios. These represent the more sophisticated end of orthodox portfolio management, where the limitations of simple mean-variance optimization are addressed through richer probabilistic frameworks.

### 6.3 Sectors, networks, and factors

The physics-informed contributions to portfolio structure come through sector identification, network analysis, and causal factor methods. Hayden, Chachra, Alemi, Ginsparg, and Sethna (S47, 2017) use unsupervised learning on return correlations to define "canonical sectors"—data-driven groupings that may differ from the standard GICS classification—and track how firm sector loadings evolve over time. This connects naturally to random matrix theory (Section 3) and to the broader question of how many independent factors drive cross-sectional returns.

Bardoscia et al. (S52, 2021) review network representations of financial systems, covering contagion models, systemic risk metrics (including DebtRank), and inference of networks from partial information. The network perspective generalizes pairwise correlations into graph structure and provides tools for understanding how shocks propagate through interconnected financial institutions—a question that became acutely practical during the 2008 crisis.

Lopez de Prado (S53, 2023) systematizes causal approaches to factor analysis, addressing the persistent challenge of distinguishing genuine risk factors from spurious correlations in the "factor zoo" of empirical asset pricing.

The hedge fund literature is represented by Strachman (S44, 2012) on industry structure and operations, and Baker and Filbeck (S51, 2021) on performance, regulation, and factor replication.

### 6.4 Suggested learning path

Start with Joshi (S45) or Bodie–Kane–Marcus (S49) for basic portfolio theory, then move to Prigent (S42) for a more comprehensive optimization treatment. Read Rebonato and Denev (S46) for stress scenarios and causal structure. Use Sethna et al. (S47) and Bardoscia et al. (S52) to move from covariance matrices to interpretable structure (sectors, networks). Lopez de Prado (S53) connects factor investing with causal identification.

---

## 7. Risk

Risk measurement and management is the section where theoretical choices about distributions and dependence structures have their most consequential practical implications. The sources here blend practitioner-facing risk texts with complex-systems and crash-modeling perspectives, unified by the theme that standard risk measures (particularly Value-at-Risk under Gaussian assumptions) systematically underestimate tail risks.

### 7.1 Tail risk and dependence

Malavergne and Sornette's *Extreme Financial Risks* (S55, 2005) models extreme events using copulas for correlation and joint distribution, addressing the critical question of tail dependence: how do extreme moves in different assets relate to one another? During market crises, correlations between assets tend to increase precisely when diversification benefits are most needed—a phenomenon that Gaussian copulas fail to capture but that more flexible dependence models can accommodate. The failure of Gaussian copula models in pricing collateralized debt obligations was, of course, a contributing factor to the 2008 financial crisis.

Dash (S54, 2004) provides C++ Monte Carlo and adjoint-method templates for modern options-desk stress scenarios—the computational infrastructure of practical risk management.

### 7.2 Model risk and epistemic humility

Rebonato's *Plight of the Fortune Tellers* (S56, 2007) critiques naïve Value-at-Risk approaches and advocates Bayesian scenario design for forward-looking stress tests. Published before the 2008 crisis, it proved prescient in its warning that standard risk models provided false confidence. Rebonato's *Bayesian Stress Testing* (S57, 2010) develops the Bayesian network framework for risk management more formally. Edwards (S59, 2014) addresses desk-level risk practice—intraday Greeks aggregation, P&L attribution—providing the operational detail that connects theoretical risk frameworks to daily trading operations.

### 7.3 Crash dynamics

Sornette's *Why Stock Markets Crash* (S60, 2017) calibrates log-periodic power-law precursors that potentially signal bubbles and crashes. This is among the more controversial contributions in the bibliography: the claim that financial crashes exhibit precursory signatures analogous to those observed before material failure or earthquakes. The methodology involves fitting log-periodic oscillations superimposed on power-law acceleration of prices, and using these fits to estimate the most probable time of a crash. The approach has both notable successes and notable failures in out-of-sample prediction, and the statistical methodology has been questioned. It remains an active area of research.

Chernov and Sornette (S62a, 2020) use hierarchical clustering to allocate tail capital across sector-specific exposures—a more applied contribution connecting crash dynamics to portfolio risk allocation. Sornette et al. (S58, 2012) provide a post-crisis reconsideration of risk modeling more broadly.

Hull's *Risk Management and Financial Institutions* (S62b, 2023) provides the regulatory context: Basel IV, CVA, and FRTB rules that shape capital requirements for financial institutions. This is the practitioner's reference for understanding the regulatory framework within which all the theoretical approaches must ultimately operate.

### 7.4 A note on numbering

The source bibliography contains numbering anomalies in this section: S61 is absent, and the label S62 is used twice (for Chernov and Sornette and for Hull). These are artifacts of the draft status of the original bibliography and are flagged here for cross-referencing purposes.

### 7.5 Suggested learning path

Start with Rebonato (S56) to calibrate expectations about what risk models can and cannot do. Pair Malavergne and Sornette (S55) with Edwards (S59) for the combination of extreme-dependence theory and desk-level practice. Use Sornette et al. (S58) and Sornette (S60) for systemic and crash-modeling perspectives. Consult Hull (S62b) for the regulatory framework.

---

## 8. Complexity Economics

The final section situates quantitative finance within the broader complexity economics paradigm. Where Sections 2 through 7 address specific technical problems—time series analysis, distribution fitting, derivative pricing, portfolio optimization—this section asks what kind of system a financial market is and what theoretical framework is appropriate for understanding it.

### 8.1 Power laws and universality

Sornette's *Theory of Zipf's Law* (S63, 2010) addresses the universality of Pareto and heavy-tailed distributions across economic and social phenomena—firm sizes, city populations, wealth distributions, word frequencies. The ubiquity of power-law distributions in economic data is one of the strongest empirical motivations for applying statistical physics methods to economics, though the interpretation of these distributions (whether they reflect genuine critical phenomena, simple stochastic processes, or measurement artifacts) remains debated.

### 8.2 Technology, innovation, and evolution

Farmer et al. (S64, 2010) model innovation diffusion as a fitness-landscape search, connecting technological evolution to ecological dynamics and real-option timing in R&D investment. Way, Lafond, Lillo, Panchenko, and Farmer (S69, 2019) develop mean-variance portfolio theory adapted to technologies whose costs decline with cumulative production (experience curves)—a creative synthesis of Markowitz portfolio theory with Wright's law of technological learning. This "Wright meets Markowitz" framework connects innovation policy with portfolio optimization in a way that neither field addresses on its own.

### 8.3 The physics-to-finance migration

Weatherall's *The Physics of Wall Street* (S65, 2013) documents the post–Cold War migration of physicists into quantitative finance—the historical narrative that underlies the entire bibliography. The migration was driven by both push factors (the end of Cold War–era physics funding, particularly in high-energy physics) and pull factors (the expansion of derivative markets and the demand for quantitative skills on Wall Street). The migrants brought with them not just technical skills but also an empirical sensibility—the insistence on checking theory against data, the comfort with heavy-tailed distributions and complex systems—that has shaped quantitative finance as a discipline. Arthur's essay on Kenneth Arrow (S68, 2018) provides complementary intellectual history, discussing informational-efficiency limits and herd behavior from the perspective of theoretical economics.

### 8.4 The complexity economics program

Arthur's *Complexity and the Economy* (S66, 2015) is the central theoretical text, outlining the non-equilibrium adaptive-expectations framework that complexity economics proposes as an alternative to neoclassical equilibrium theory. In this view, economic agents do not have access to the full rational-expectations equilibrium; instead, they form expectations adaptively, using simple heuristics and learning rules, and the aggregate behavior that emerges from their interactions is generically out of equilibrium. Arthur argues that this framework naturally generates phenomena—implied-volatility smiles, demand imbalances, bubbles, crashes—that appear as puzzles or anomalies within the equilibrium paradigm.

Gatti et al. (S67, 2018) provide the computational toolkit: scalable agent-based modeling (ABM) frameworks for policy analysis and liquidity cascades. Agent-based models are the natural computational embodiment of the complexity economics worldview—they simulate the interactions of heterogeneous agents according to specified behavioral rules and study the emergent aggregate dynamics. The challenge is that ABMs are easy to build and hard to validate: the space of possible agent specifications is enormous, and connecting ABM output to empirical data in a disciplined way remains an open methodological problem.

Farmer's *Making Sense of Chaos* (S70, 2024) represents the intellectual culmination of the physics-to-finance migration documented throughout the bibliography. Three decades after leaving physics for finance, Farmer synthesizes his research program into a roadmap for complexity economics—an argument that the tools of complexity science (agent-based modeling, network theory, evolutionary dynamics, machine learning) are ready to address problems where orthodox economics has struggled.

### 8.5 Suggested learning path

Read Farmer (S70) as a modern synthesis, then use the Santa Fe Institute working papers (S64, S69) for concrete applications of technology/portfolio analysis. Gatti et al. (S67) provides the ABM technical toolkit. Arthur (S66) is the theoretical foundation. Weatherall (S65) is context-setting history.

---

## 9. Cross-Cutting Themes

Several structural themes emerge from reading across the seven sections. These themes provide the intellectual coherence that makes this collection more than a list of references.

### 9.1 The empirics-first ethos

The most distinctive feature of the physics-informed approach to finance is its insistence on taking empirical data seriously as a constraint on theory. Fat-tailed return distributions, volatility clustering, long-memory in order flow, the square-root law of market impact, power-law distributions of firm sizes and wealth—these stylized facts are documented across multiple sources and time periods, and they collectively rule out the Gaussian assumptions that underlie much of orthodox financial economics. The physics approach does not necessarily provide better predictions than the orthodox approach, but it provides models that are at least consistent with what the data show.

### 9.2 Multi-scale structure

The bibliography spans multiple scales: microsecond tick data (S32–S35), daily returns (S14, S15), and macroeconomic phenomena (S66, S67). The scaling relationships connecting these levels—how microstructure generates the statistical properties observed at longer horizons—constitute a distinctive contribution of the physics methodology. The multifractal analysis of Section 3 (S24) provides the mathematical framework for characterizing these cross-scale relationships.

### 9.3 Methodological pluralism

Three methodological traditions are represented: statistical/empirical approaches documenting stylized facts, stochastic modeling extending Black-Scholes with non-Gaussian processes, and agent-based computational models. The bibliography suggests these approaches are complementary rather than competing. Empirical measurement constrains the models; stochastic models provide tractable pricing and hedging tools; agent-based models generate the empirical regularities from plausible micro-level dynamics.

### 9.4 The Santa Fe Institute influence

Multiple sources connect to the Santa Fe Institute's complexity research program (S23, S64, S70). This institutional locus shaped the methodological horizons of econophysics, emphasizing adaptive systems, evolutionary dynamics, and computational approaches. The SFI connection also explains the persistent interest in agent-based modeling and ecological dynamics that distinguishes this literature from more conventional quantitative finance.

### 9.5 Practitioners as theorists

A notable feature of the bibliography is the prominence of practitioner-academics: Jean-Philippe Bouchaud (Capital Fund Management), J. Doyne Farmer (originally at Prediction Company, now at Oxford), and Didier Sornette (ETH Zürich with extensive consulting). These figures have contributed both to theoretical development and to practical implementation, and their work reflects a productive tension between the demands of academic rigor and the constraints of real-world trading.

---

## 10. Assessment and Future Directions

### 10.1 Strengths of the collection

The bibliography provides comprehensive coverage of foundational and contemporary literature in econophysics and computational finance. Its organizational structure—progressing from data through theory to applications and synthesis—mirrors the logical structure of the subject. The balance between physics-based and traditional finance perspectives ensures that the reader encounters the orthodox view alongside the alternatives, enabling informed comparison rather than partisan advocacy. The inclusion of historical and philosophical context (Schinckus, Weatherall) is unusual and valuable: it is rare for a technical bibliography to situate its contents within a broader intellectual narrative.

The emphasis on empirically-grounded approaches over pure theory is appropriate given the state of the field. The mix of ArXiv preprints and peer-reviewed monographs ensures both accessibility (many preprints are freely available) and rigor (the major Cambridge, Princeton, and Springer texts have undergone editorial review).

### 10.2 Limitations and gaps

Several areas are underrepresented relative to current practice. High-frequency trading and algorithmic market-making research—the Avellaneda-Stoikov framework, optimal execution under adverse selection, latency arbitrage—is not deeply covered despite being a major area of quantitative finance. Machine learning applications, while gestured at (S7, S12), are thin relative to the explosive growth of ML methods in finance over the past decade. Fixed-income term-structure modeling beyond PCA appears only through a single Rebonato text (S48). Behavioral finance is represented primarily through Pompian (S31) and could be expanded to include the substantial academic literature on limits to arbitrage, sentiment, and informed trading. Cryptocurrency and decentralized finance are entirely absent—a reasonable omission given the physics-informed emphasis, but one the reader should note.

Several publisher links in the original bibliography point to paywalled content. Where possible, ArXiv preprints or institutional repositories provide alternative access, but some major texts (particularly from Wiley and Princeton Press) may require library access.

### 10.3 Connections to other chapters

This chapter connects to several other sections of *Projects in Scientific Computing*. The stochastic calculus chapter provides the mathematical foundations for continuous-time asset pricing (Section 5) and SPDE models of order books (Section 4). The fractional calculus notes support the α-stable Lévy processes and fractional diffusions that appear in non-Gaussian derivative pricing (S39, S41). The path integrals chapter provides background for the field-theoretic methods that appear in spin-glass approaches to financial data (S28). The option trading notes complement the risk and derivative pricing material here with more applied content. These cross-connections are a central feature of the project: the same mathematical structures appear in physics and finance, and understanding them in one context illuminates the other.

---

**Bibliography**

## 1. Data: Time Series Analysis  

| ID | Source | Notes |
|---|---|---|
| S1 | [Farmer & Sidorowich, *Predicting Chaotic Time Series* (1987)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.59.845) | Pioneers phase-space embedding and short-horizon chaos forecasts. |
| S2 | [Farmer, *Nonlinearity in Time Series* (1992)](https://www.doynefarmer.com/machine-learning-and-data-analysis) | Shows low-dimensional deterministic structures. |
| S3 | [Hamilton, *Time-Series Analysis* (1994)](https://press.princeton.edu/books/hardcover/9780691042893/time-series-analysis) | Classic reference with abundant source materal. |
| S4 | [Campbell – Lo – MacKinlay, *Econometrics of Financial Markets* (1997)](https://press.princeton.edu/books/hardcover/9780691043012/the-econometrics-of-financial-markets) | Formalises spectral tests, long-memory diagnostics, and GMM baselines for empirical factor models. |
| S5 | [Cochrane, *Time Series for Macroeconomics and Finance* (1997)](https://www.smartquant.com/references/TimeSeries/ts13.pdf) | Connects discrete-time VAR/GMM estimation with continuous-time pricing kernels. |
| S6 | [Kantz & Schreiber, *Nonlinear Time-Series Analysis* (2004)](https://www.cambridge.org/core/books/nonlinear-time-series-analysis/519783E4E8A2C3DCD4641E42765309C7) | Details surrogate-data tests. |
| S7 | [Adhikari & Agrawal, *Time-Series Neural Networks* (2013)](https://arxiv.org/abs/1302.6613) | Performance comparison of stochastic models, early neural nets, and SVM. |
| S8 | [Bradley & Kantz, *Nonlinear Time-Series* (2015)](https://arxiv.org/abs/1503.07493) | History of nonlinear time series analysis. |
| S10 | [Ruey & Chen, *Nonlinear Time-Series* (2019)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119514312) |Survey of methods for approaching nonlinearity. |
| S11 | [Marcaccioli & Livan, *Stat-Mech Time Series* (2019)](https://arxiv.org/pdf/2003.12818) | Applies Boltzman statistical mechanics directly to time series. |
| S12 | [Ekapure et al, *Technical Analysis Meets Data Science* (2021)](https://arxiv.org/abs/2107.14695) | Applies machine learing directly to trend classification. |

---

## 2. Data: Empirical Stylized Facts   

| ID | Source | Notes |
|---|---|---|
| S13 | [Di Francesco *et al.*, *Random Matrices* (1994)](https://arxiv.org/abs/hep-th/9306153) | Random-matrix theory and low dimensional quantum fields. |
| S14 | [Mantegna & Stanley, *Introduction to Econophysics* (2000)](https://www.cambridge.org/core/books/introduction-to-econophysics/6A2727FE42578790E6E1021B7955EE30) | Introductory text viewing financial data from the perspective of statistical physics. |
| S15 | [Mandelbrot, *The Misbehavior of Markets* (2004)](https://www.amazon.com/Misbehavior-Markets-annotated-Benoit-Mandelbrot/dp/B0077T2DIY) | Argues for fractal scaling and α-stable processes over Gaussian assumptions. |
| S16 | [Farmer et al, *Is Economics the Next Physical Science?* (2005)](https://pubs.aip.org/physicstoday/article-abstract/58/9/37/399433/Is-Economics-the-Next-Physical-Science-An-emerging?redirectedFrom=fulltext) | Advocates physicists’ universality concepts for financial innovation. |
| S17 | [Yakovenko, *Econophysics* (2008)](https://arxiv.org/abs/0709.3662) | Review of the literature and methods. |
| S18 | [Chakraborti *et al*, *Econophysics* (2010)](https://arxiv.org/abs/0909.1974) | Review of the literatute and methods. |
| S19 | [Chakrabarti *et al.*, *Econophysics* (2012)](https://www.jstor.org/stable/23251800) | Review of the literature and methods. |
| S20 | [Chakraborti *et al.*, *Econophysics* (2013)](https://link.springer.com/chapter/10.1007/978-3-319-08473-2_11) | Review of the literature and methods. |
| S21 | [Sornette, *Econophysics* (2014)](https://arxiv.org/abs/1404.0243) | Review of the literature and methods. |
| S22 | [Abergel et al, *Econophysics & Sociophysics* (2017)](https://link.springer.com/book/10.1007/978-3-319-47705-3) | Expansion to social networks, diffusion, and power laws. |
| S23 | [Schinkus, *A History of Econophysics* (2018)](https://www.repository.cam.ac.uk/items/61fb15c9-7e20-4229-9327-5213a3916356) | PhD disseration history and philosophy of science. Complex systems, Sante Fe Institute.  |
| S24 | [Sornette, *Multifractals in Finance* (2018)](https://arxiv.org/abs/1805.04750) | Deep dive into multifractal analysis of financial data. |
| S25 | [Bouchaud, *Econophysics* (2019)](https://arxiv.org/abs/1901.03691) | Review of the literature and methods. |
| S26 | [Abergel *et al.*, *Econophysics & Sociophysics* (2019)](https://link.springer.com/book/10.1007/978-3-030-11364-3) | Includes social networks, diffusion and dynamics. |
| S27 | [Potters & Bouchaud, *A First Course in Random-Matrix Theory* (2020)](https://www.cambridge.org/core/books/first-course-in-random-matrix-theory/2292A554A9BB9E2A4697C35BCE920304) | Foundations of RMT with applications to covariance of assets. |
| S28 | [Bouchaud et al, *Spin-Glass Markets* (2023)](https://arxiv.org/abs/2306.16165) | Spin glass methods (replica, replica symmetry breaking, cavity method) applied to generic complex data. |

---

## 3. Data: Market Microstructures 

| ID | Source | Notes |
|---|---|---|
| S29 | [Farmer, *Slippage* (1996)](https://oms-inet.files.svdcdn.com/production/files/slippage.pdf) | Introduction to market-impact cost functions. |
| S30 | [Farmer *Market Ecology & Evolution* (1998)](https://arxiv.org/abs/adap-org/9812005) | Models trader populations with Lotka–Volterra dynamics to explain clustered volatility and intraday skew shifts. |
| S31 | [Pompian et al, *Behavioral Finance* (2006)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119202400) | Catalogues cognitive biases that leak into demand‐pressure anomalies exploitable via volatility and skew trades. |
| S32 | [Abergel, *Limit Order Books* (2016)](https://www.cambridge.org/us/universitypress/subjects/mathematics/mathematical-finance/limit-order-books?format=HB&isbn=9781107163980) | Empirical order-book stylised facts aand agent based models. |
| S33 | [Lehalle & Laruelle, *Market Microstructure* (2018)](https://www.worldscientific.com/worldscibooks/10.1142/10739) | Calibrates Market impact, order-flow clustering, liquidity, regulation, and persistence. |
| S34 | [Bouchaud *et al.*, *Trades, Quotes & Prices* (2018)](https://www.cambridge.org/core/books/trades-quotes-and-prices/029A71078EE4C41C0D5D4574211AB1B5) | Market impact, order-flow, liquidity. |
| S35 | [Cont & Mueller, *SPDEs for Limit-Order Books* (2020)](https://arxiv.org/abs/1904.03058) | Introduces stochastic-PDE modeling of limit order books. |

---

## 4. Asset Pricing Theory

| ID | Source | Notes |
|---|---|---|
| S36 | [Tracy, *How to Read a Financial Report* (1999)](https://www.wiley.com/en-us/How+to+Read+a+Financial+Report%3A+Wringing+Vital+Signs+Out+of+the+Numbers%2C+10th+Edition-p-9781394268719) | Distils accounting statements into key cash-flow and leverage signals often engineered as factors in option-carry models. |
| S37 | [Cochrane, *Asset Pricing* (2000)](https://press.princeton.edu/books/hardcover/9780691121376/asset-pricing) | Derives the stochastic-discount-factor framework central to risk-neutral valuation. |
| S38 | [Duffie, *Dynamic Asset-Pricing Theory* (2001)](https://press.princeton.edu/books/hardcover/9780691090221/dynamic-asset-pricing-theory) | Itô-calculus proofs for optimal-exercise boundaries and contingent-claim valuation in continuous time. |
| S39 | [Bouchaud & Potters, *Theory of Financial Risk & Derivative Pricing* (2003)](https://www.cambridge.org/core/books/theory-of-financial-risk-and-derivative-pricing/5BBBA04CE72ED9E5E7C1C028D9A94FCB) | Integrates heavy-tailed return statistics into Black–Scholes-type PDEs via fractional diffusions. |
| S40 | [Voit  *Statistical Mechanics of Financial Markets* (2005)](https://link.springer.com/book/10.1007/b137351) | Statistical methods applied broadly to quantiative finance. |
| S41 | [Kleinert, *L'evy Option Pricing* (2016)](https://arxiv.org/abs/1611.04320) | Alpha stable L'evy processes calibrated to the market. |

---

## 5. Multi-Asset Structures and Factor Analysis  

| ID | Source | Notes |
|---|---|---|
| S42 | [Prigent, *Portfolio Optimization* (2007)](https://www.routledge.com/Portfolio-Optimization-and-Performance-Analysis/Prigent/p/book/9781584885788) | Presents quadratic-programming routines for mean-variance allocation with option and transaction-cost constraints. |
| S43 | [Peters, *Ergodicity & the Kelly Criterion* (2010)](https://arxiv.org/abs/0902.2965) | Justifies growth-optimal position sizing and leverage control for volatility-targeting strategies. |
| S44 | [Strachman, *Hedge-Fund Management* (2012)](https://www.wiley.com/en-us/The+Fundamentals+of+Hedge+Fund+Management%3A+How+to+Successfully+Launch+and+Operate+a+Hedge+Fund%2C+2nd+Edition-p-9781118239230) | Industry, regulation, structure, accounting, marketing, risk management. |
| S45 | [Joshi, *Mathematical Portfolio Theory* (2013)](https://www.cambridge.org/us/universitypress/subjects/mathematics/optimization-or-and-risk-analysis/introduction-mathematical-portfolio-theory?format=HB&isbn=9781107042315) | Neoclassical approach to efficient frontier. |
| S46 | [Rebonato & Denev, *Portfolio Management under Stress* (2013)](https://www.cambridge.org/core/books/portfolio-management-under-stress/481A8284865AAF4894011413D5E2D487) | Uses Bayesian networks for asset allocation. |
| S47 | [Sethna, *Statistical Mechanics of Market Sectors* (2017)](https://arxiv.org/abs/1503.06205) | Canonical sectors from unsupervised learning. |
| S48 | [Rebonato, *Bond Pricing & Yield-Curve Modeling* (2018)](https://www.cambridge.org/core/books/bond-pricing-and-yield-curve-modeling/8BD16E2AC2B8CB6248A151F4BD5D25E8) | Presents PCA-driven term-structure dynamics. |
| S49 | [Bodie, Kane & Marcus, *Investments* (2018)](https://www.mheducation.com/highered/product/Investments-Bodie.html) | Neoclassical view including CAPM and APT. |
| S50 | [Brealey, Myers & Allen, *Principles of Corporate Finance* (2019)](https://www.mheducation.com/highered/product/Principles-of-Corporate-Finance-Brealey.html) | Neoclassical approach to corporate capital-budgeting decisions and project flexibilities. |
| S51 | [Baker & Filbeck, *Hedge Funds* (2021)](https://academic.oup.com/book/25365) | Performance, regulation, and factor replication techniques across global hedge-fund sector. |
| S52 | [Bardoscia *et al.*, *Financial Networks* (2021)](https://arxiv.org/abs/2103.05623) | Dynamical evolution of financial networks. |
| S53 | [Lopez de Prado, *Causal Factor Investing* (2023)](https://www.cambridge.org/core/elements/causal-factor-investing/9AFE270D7099B787B8FD4F4CBADE0C6E) | Systematization of factor analysis. |

---
## 6. Risk 

| ID | Source | Notes |
|---|---|---|
| S54 | [Dash, *Quantitative Finance & Risk Management* (2004)](https://www.worldscientific.com/worldscibooks/10.1142/9003) | Supplies C++ Monte-Carlo and adjoint-method templates that form the engine of modern options-desk stress scenarios. |
| S55 | [Malavergne & Sornette, *Extreme Financial Risks* (2005)](https://link.springer.com/book/10.1007/b138841) | Extreme shocks with contagion modeled with copulas for correlation and joint distribution. |
| S56 | [Rebonato, *Plight of the Fortune Tellers* (2007)](https://press.princeton.edu/books/paperback/9780691148175/plight-of-the-fortune-tellers) | Critiques naïve VaR and advocates Bayesian scenario design for forward-looking stress tests. |
| S57 | [Rebonato, *Bayesian Stress Testing* (2010)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118374719) | Uses bayesian nets for risk. |
| S58 | [Sornette et al, *Risk & Market Modeling* (2012)](https://link.springer.com/book/10.1007/978-3-642-27931-7) | Post financial crisis reconsideration of risk. |
| S59 | [Edwards, *Risk Management in Trading* (2014)](https://www.wiley.com/en-us/Risk+Management+in+Trading%3A+Techniques+to+Drive+Profitability+of+Hedge+Funds+and+Trading+Desks-p-9781118768587) | Details intraday Greeks aggregation and P&L attribution crucial for volatility-arbitrage desks. |
| S60 | [Sornette, *Why Stock Markets Crash* (2017)](https://press.princeton.edu/books/paperback/9780691175959/why-stock-markets-crash) | Calibrates log-periodic power-law precursors that signal bubbles and crashes. |
| S62 | [Chernov & Sornette, *Risks of Economic Sectors* (2020)](https://link.springer.com/book/10.1007/978-3-030-25034-8) | Uses hierarchical clustering to allocate tail capital across sector-specific option exposures. |
| S62 | [Hull, *Risk Management & Financial Institutions* (2023)](https://www.wiley.com/en-us/Risk+Management+and+Financial+Institutions%2C+6th+Edition-p-9781119932482) | Summarises Basel IV CVA and FRTB rules that directly shape capital for option-market makers. |

---
## 7. Complexity Economics   

| ID | Source | Notes |
|---|---|---|
| S63 | [Sornette, *Theory of Zipf’s Law* (2010)](https://link.springer.com/book/10.1007/978-3-642-02946-2) | Universality of Pareto and heavy-tailed distributions. |
| S64 | [Farmer et al, *The Evolutionary Ecology of Technology* (2010)](https://www.santafe.edu/research/results/working-papers/the-evolutionary-ecology-of-technological-innovati) | Models innovation diffusion as a fitness-landscape search, mirroring real-option timing games in R&D. |
| S65 | [Weatherall, *The Physics of Wall Street* (2013)](https://www.amazon.com/Physics-Wall-Street-Predicting-Unpredictable/dp/0547317271) | History and philosophy of science. Migration, post cold war, of physicists to computational finance / financial engineering. |
| S66 | [Arthur, *Complexity & the Economy* (2015)](https://global.oup.com/academic/product/complexity-and-the-economy-9780199334292) | Outlines non-equilibrium adaptive expectations underlying implied-volatility smiles and demand imbalances. |
| S67 | [Gatti et al, *Agent-Based Models in Economics* (2018)](https://www.cambridge.org/core/books/agentbased-models-in-economics/E4FB7268269E7BCB8CE8E45894D105CC) | Provides scalable ABM code for policy shocks and liquidity cascades in financial and economic markets. |
| S68 | [Arthur, *Kenneth Arrow’s Contributions to Finance* (2018)](https://www.tandfonline.com/doi/pdf/10.1080/14697688.2018.1533738) | Discusses informational-efficiency limits and herd behaviour relevant to behavioural option flows. |
| S69 | [Farmer et al, *Technology Portfolios & Complex Networks* (2019)](https://arxiv.org/abs/1705.03423) | Uses network centrality to allocate real-option bets across technological domains and patent clusters. |
| S70 | [Farmer, *Making Sense of Chaos* (2024)](https://yalebooks.yale.edu/book/9780300283327/making-sense-of-chaos/) | Synthesis of three decades of complexity research into a roadmap for complexity economics. |
