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
Resources in quantatitive finance are provided.  Emphasis is given to statistical analysis of empirical stylized facts. For completeness, the orthodox neoclassical view of asset pricing, portfolio theory, and risk is included.

## 1 Time Series Analysis  

| ID | Source | Notes |
|---|---|---|
| **S1** | [Farmer & Sidorowich, *Predicting Chaotic Time Series* (1987)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.59.845) | Pioneers phase-space embedding and short-horizon chaos forecasts. |
| **S2** | [Farmer, *Nonlinearity in Time Series* (1992)](https://www.doynefarmer.com/machine-learning-and-data-analysis) | Shows low-dimensional deterministic structures. |
| **S3** | [Hamilton, *Time-Series Analysis* (1994)](https://press.princeton.edu/books/hardcover/9780691042893/time-series-analysis) | Provides Kalman-filter and Markov-switching machinery that underpins stochastic-volatility surface estimation. |
| **S4** | [Campbell – Lo – MacKinlay, *Econometrics of Financial Markets* (1997)](https://press.princeton.edu/books/hardcover/9780691043012/the-econometrics-of-financial-markets) | Formalises spectral tests, long-memory diagnostics, and GMM baselines for empirical factor models. |
| **S5** | [Cochrane, *Time Series for Macroeconomics and Finance* (1997)](https://www.smartquant.com/references/TimeSeries/ts13.pdf) | Connects discrete-time VAR/GMM estimation with continuous-time pricing kernels. |
| **S6** | [Kantz & Schreiber, *Nonlinear Time-Series Analysis* (2004)](https://www.cambridge.org/core/books/nonlinear-time-series-analysis/519783E4E8A2C3DCD4641E42765309C7) | Details surrogate-data tests. |
| **S7** | [Adhikari & Agrawal.*, *Time-Series Neural Networks* (2013)](https://arxiv.org/abs/1302.6613) | Performance comparison of stochastic models, early neural nets, and SVM. |
| **S8** | [Bradley & Kantz, *Nonlinear Time-Series* (2015)](https://arxiv.org/abs/1503.07493) | History of nonlinear time series analysis. |
| **S10** | [Ruey & Chen, *Nonlinear Time-Series* (2019)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119514312) |Survey of methods for approaching nonlinearity. |
| **S11** | [Marcaccioli & Livan*, *Stat-Mech Time Series* (2019)](https://arxiv.org/pdf/2003.12818) | Applies Boltzman statistical mechanics directly to time series. |
| **S12** | [Ekapure et al, *Technical Analysis Meets Data Science* (2021)](https://arxiv.org/abs/2107.14695) | Applies machine learing directly to trend classification. |

---

## 2 Asset Pricing Theory

| ID | Source | Notes |
|---|---|---|
| **S13** | [Cochrane, *Asset Pricing* (2000)](https://press.princeton.edu/books/hardcover/9780691121376/asset-pricing) | Derives the stochastic-discount-factor framework central to risk-neutral valuation. |
| **S14** | [Duffie, *Dynamic Asset-Pricing Theory* (2001)](https://press.princeton.edu/books/hardcover/9780691090221/dynamic-asset-pricing-theory) | Itô-calculus proofs for optimal-exercise boundaries and contingent-claim valuation in continuous time. |
| **S15** | [Bouchaud & Potters, *Theory of Financial Risk & Derivative Pricing* (2003)](https://www.cambridge.org/core/books/theory-of-financial-risk-and-derivative-pricing/5BBBA04CE72ED9E5E7C1C028D9A94FCB) | Integrates heavy-tailed return statistics into Black–Scholes-type PDEs via fractional diffusions. |
| **S16** | [Voit  *Statistical Mechanics of Financial Markets* (2005)](https://link.springer.com/book/10.1007/b137351) | Statistical methods applied broadly to quantiative finance. |
| **S17** | [Kleinert, *Path Integrals in Option Pricing* (2016)](https://arxiv.org/abs/1611.04320) | Pricing under alpha stable Levy processes. |
| **S18** | [Rebonato, *Bond Pricing & Yield-Curve Modeling* (2018)](https://www.cambridge.org/core/books/bond-pricing-and-yield-curve-modeling/8BD16E2AC2B8CB6248A151F4BD5D25E8) | Presents PCA-driven term-structure dynamics that feed directly into swaption and Bermudan pricing engines. |
| **S51** | [Tracy, *How to Read a Financial Report* (1999)](https://www.wiley.com/en-us/How+to+Read+a+Financial+Report%3A+Wringing+Vital+Signs+Out+of+the+Numbers%2C+10th+Edition-p-9781394268719) | Distils accounting statements into key cash-flow and leverage signals often engineered as factors in option-carry models. |

---

## 3 Financial Data: Stylized Facts   

| ID | Source | Notes |
|---|---|---|
| **S19** | [Di Francesco *et al.*, *Random Matrices* (1994)](https://arxiv.org/abs/hep-th/9306153) | Random-matrix theory. |
| **S20** | [Mantegna & Stanley, *Introduction to Econophysics* (2000)](https://www.cambridge.org/core/books/introduction-to-econophysics/6A2727FE42578790E6E1021B7955EE30) | Introductory text viewing financial data from the perspective of statistical physics. |
| **S21** | [Mandelbrot, *The Misbehavior of Markets* (2004)](https://www.amazon.com/Misbehavior-Markets-annotated-Benoit-Mandelbrot/dp/B0077T2DIY) | Argues for fractal scaling and α-stable processes over Gaussian assumptions. |
| **S22** | [Farmer et al, *Is Economics the Next Physical Science?* (2005)](https://pubs.aip.org/physicstoday/article-abstract/58/9/37/399433/Is-Economics-the-Next-Physical-Science-An-emerging?redirectedFrom=fulltext) | Advocates physicists’ universality concepts for financial innovation. |
| **S23** | [Yakovenko, *Stat-Mech Econophysics* (2008)](https://arxiv.org/abs/0709.3662) | 20 year review of the literature and methods. |
| **S24** | [Chakraborti et al, *Econophysics: Kinetic-Exchange Models* (2010)](https://arxiv.org/abs/0909.1974) | Review of the literatute and methods. |
| **S25** | [Chakrabarti *et al.*, *Econophysics* (2012)](https://www.jstor.org/stable/23251800) | Review of the literature and methods. |
| **S26** | [Chakraborti *et al.*, *Econophysicss* (2013)](https://link.springer.com/chapter/10.1007/978-3-319-08473-2_11) | Review of the literature and methods. |
| **S27** | [Sornette, *Econophysics: A Review* (2014)](https://arxiv.org/abs/1404.0243) | Review of the literature and methods. |
| **S28** | [Abergel et al, *Econophysics & Sociophysics* (2017)](https://link.springer.com/book/10.1007/978-3-319-47705-3) | Expansion to social networks, diffusion, and power laws. |
| **S29** | [Schinkus, *A History of Econophysics* (2018)](https://www.repository.cam.ac.uk/items/61fb15c9-7e20-4229-9327-5213a3916356) | PhD disseration history and philosophy of science. Complex systems, Sante Fe Institute.  |
| **S30** | [Sornette, *Multifractals in Finance* (2018)](https://arxiv.org/abs/1805.04750) | Deep dive into multifractal analysis of financial data. |
| **S31** | [Bouchaud, *Econophysics* (2019)](https://arxiv.org/abs/1901.03691) | 30 year review of the literature and methods. |
| **S32** | [Abergel *et al.*, *Econophysics & Sociophysics* (2019)](https://link.springer.com/book/10.1007/978-3-030-11364-3) | Includes social networks, diffusion and dynamics. |
| **S33** | [Potters & Bouchaud, *A First Course in Random-Matrix Theory* (2020)](https://www.cambridge.org/core/books/first-course-in-random-matrix-theory/2292A554A9BB9E2A4697C35BCE920304) | Foundations of RMT with applications to covariance. |
| **S34** | [Bouchaud et al, *Spin-Glass Markets* (2023)](https://arxiv.org/abs/2306.16165) | Spin glass methods (replica, replica symmetry breaking, cavity method) applied to generic complex data. |

---
## 4 Market Microstructures 

| ID | Source | Notes |
|---|---|---|
| **S35** | [Farmer, *Slippage* (1996)](https://oms-inet.files.svdcdn.com/production/files/slippage.pdf) | Introduction to market-impact cost functions. |
| **S36** | [Farmer *Market Ecology & Evolution* (1998)](https://arxiv.org/abs/adap-org/9812005) | Models trader populations with Lotka–Volterra dynamics to explain clustered volatility and intraday skew shifts. |
| **S52** | [Pompian et al, *Behavioral Finance* (2006)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119202400) | Catalogues cognitive biases that leak into demand‐pressure anomalies exploitable via volatility and skew trades. |
| **S37** | [Abergel, *Limit Order Books* (2016)](https://www.cambridge.org/us/universitypress/subjects/mathematics/mathematical-finance/limit-order-books?format=HB&isbn=9781107163980) | Empirical order-book stylised facts aand agent based models. |
| **S38** | [Lehalle & Laruelle, *Market Microstructure* (2018)](https://www.worldscientific.com/worldscibooks/10.1142/10739) | Calibrates Market impact, order-flow clustering, liquidity, regulation, and persistence. |
| **S39** | [Bouchaud *et al.*, *Trades, Quotes & Prices* (2018)](https://www.cambridge.org/core/books/trades-quotes-and-prices/029A71078EE4C41C0D5D4574211AB1B5) | Market impact, order-flow, liquidity. |
| **S40** | [Cont & Mueller, *SPDEs for Limit-Order Books* (2020)](https://arxiv.org/abs/1904.03058) | Introduces stochastic-PDE modeling of limit order books. |

---

## 5 Multi-Asset Structures and Factor Analysis  

| ID | Source | Notes |
|---|---|---|
| **S9** | [Sethna, *Statistical Mechanics of Inference* (2017)](https://arxiv.org/abs/1503.06205) | Canonical sectors from unsupervised learning. |
| **S49** | [Bardoscia *et al.*, *Financial Networks* (2021)](https://arxiv.org/abs/2103.05623) | Dynamical evolution of financial networks. |
| **S53** | [Prigent, *Portfolio Optimization* (2007)](https://www.routledge.com/Portfolio-Optimization-and-Performance-Analysis/Prigent/p/book/9781584885788) | Presents quadratic-programming routines for mean-variance allocation with option and transaction-cost constraints. |
| **S54** | [Peters, *Ergodicity & the Kelly Criterion* (2010)](https://arxiv.org/abs/0902.2965) | Justifies growth-optimal position sizing and leverage control for volatility-targeting strategies. |
| **S55** | [Strachman, *Hedge-Fund Management* (2012)](https://www.wiley.com/en-us/The+Fundamentals+of+Hedge+Fund+Management%3A+How+to+Successfully+Launch+and+Operate+a+Hedge+Fund%2C+2nd+Edition-p-9781118239230) | Industry, regulation, structure, accounting, marketing, risk management. |
| **S56** | [Joshi, *Mathematical Portfolio Theory* (2013)](https://www.cambridge.org/us/universitypress/subjects/mathematics/optimization-or-and-risk-analysis/introduction-mathematical-portfolio-theory?format=HB&isbn=9781107042315) | Neoclassical approach to efficient frontier. |
| **S57** | [Rebonato & Denev, *Portfolio Management under Stress* (2013)](https://www.cambridge.org/core/books/portfolio-management-under-stress/481A8284865AAF4894011413D5E2D487) | Uses Bayesian networks for asset allocation. |
| **S58** | [Baker & Filbeck, *Hedge Funds* (2021)](https://academic.oup.com/book/25365) | Performance, regulation, and factor replication techniques across global hedge-fund sector. |
| **S59** | [Bodie, Kane & Marcus, *Investments* (2018)](https://www.mheducation.com/highered/product/Investments-Bodie.html) | Neoclassical view including CAPM and APT. |
| **S60** | [Brealey, Myers & Allen, *Principles of Corporate Finance* (2019)](https://www.mheducation.com/highered/product/Principles-of-Corporate-Finance-Brealey.html) | Neoclassical approach to corporate capital-budgeting decisions and project flexibilities. |
| **S61** | [Lopez de Prado, *Causal Factor Investing* (2023)](https://www.cambridge.org/core/elements/causal-factor-investing/9AFE270D7099B787B8FD4F4CBADE0C6E) | Systematization of factor analysis. |

---
## 6 Risk 

| ID | Source | Notes |
|---|---|---|
| **S41** | [Dash, *Quantitative Finance & Risk Management* (2004)](https://www.worldscientific.com/worldscibooks/10.1142/9003) | Supplies C++ Monte-Carlo and adjoint-method templates that form the engine of modern options-desk stress scenarios. |
| **S42** | [Malavergne & Sornette, *Extreme Financial Risks* (2005)](https://link.springer.com/book/10.1007/b138841) | Extreme shocks with contagion modeled with copulas for correlation and joint distribution. |
| **S43** | [Rebonato, *Plight of the Fortune Tellers* (2007)](https://press.princeton.edu/books/paperback/9780691148175/plight-of-the-fortune-tellers) | Critiques naïve VaR and advocates Bayesian scenario design for forward-looking stress tests. |
| **S44** | [Rebonato, *Bayesian Stress Testing* (2010)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118374719) | Uses bayesian nets for risk. |
| **S45** | [Sornette et al, *Risk & Market Modeling* (2012)](https://link.springer.com/book/10.1007/978-3-642-27931-7) | Post financial crisis reconsideration of risk. |
| **S46** | [Edwards, *Risk Management in Trading* (2014)](https://www.wiley.com/en-us/Risk+Management+in+Trading%3A+Techniques+to+Drive+Profitability+of+Hedge+Funds+and+Trading+Desks-p-9781118768587) | Details intraday Greeks aggregation and P&L attribution crucial for volatility-arbitrage desks. |
| **S47** | [Sornette, *Why Stock Markets Crash* (2017)](https://press.princeton.edu/books/paperback/9780691175959/why-stock-markets-crash) | Calibrates log-periodic power-law precursors that signal bubbles and crashes. |
| **S48** | [Chernov & Sornette, *Risks of Economic Sectors* (2020)](https://link.springer.com/book/10.1007/978-3-030-25034-8) | Uses hierarchical clustering to allocate tail capital across sector-specific option exposures. |
| **S50** | [Hull, *Risk Management & Financial Institutions* (2023)](https://www.wiley.com/en-us/Risk+Management+and+Financial+Institutions%2C+6th+Edition-p-9781119932482) | Summarises Basel IV CVA and FRTB rules that directly shape capital for option-market makers. |

---
## 7 Complexity Economics   

| ID | Source | Notes |
|---|---|---|
| **S62** | [Sornette, *Theory of Zipf’s Law* (2010)](https://link.springer.com/book/10.1007/978-3-642-02946-2) | Universality of Pareto and heavy-tailed distributions. |
| **S63** | [Farmer et al, *The Evolutionary Ecology of Technology* (2010)](https://www.santafe.edu/research/results/working-papers/the-evolutionary-ecology-of-technological-innovati) | Models innovation diffusion as a fitness-landscape search, mirroring real-option timing games in R&D. |
| **S64** | [Weatherall, *The Physics of Wall Street* (2013)](https://www.amazon.com/Physics-Wall-Street-Predicting-Unpredictable/dp/0547317271) | History and philosophy of science. Migration, post cold war, of physicists to computational finance / financial engineering. |
| **S65** | [Arthur, *Complexity & the Economy* (2015)](https://global.oup.com/academic/product/complexity-and-the-economy-9780199334292) | Outlines non-equilibrium adaptive expectations underlying implied-volatility smiles and demand imbalances. |
| **S66** | [Gatti et al, *Agent-Based Models in Economics* (2018)](https://www.cambridge.org/core/books/agentbased-models-in-economics/E4FB7268269E7BCB8CE8E45894D105CC) | Provides scalable ABM code for policy shocks and liquidity cascades in financial and economic markets. |
| **S67** | [Arthur, *Kenneth Arrow’s Contributions to Finance* (2018)](https://www.tandfonline.com/doi/pdf/10.1080/14697688.2018.1533738) | Discusses informational-efficiency limits and herd behaviour relevant to behavioural option flows. |
| **S68** | [Farmer et al, *Technology Portfolios & Complex Networks* (2019)](https://arxiv.org/abs/1705.03423) | Uses network centrality to allocate real-option bets across technological domains and patent clusters. |
| **S69** | [Farmer, *Making Sense of Chaos* (2024)](https://yalebooks.yale.edu/book/9780300283327/making-sense-of-chaos/) | Synthesis of three decades of complexity research into a roadmap for complexity economics. |