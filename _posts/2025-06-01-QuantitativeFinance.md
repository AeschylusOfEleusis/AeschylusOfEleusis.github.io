---
layout:   post
title: "Quantitative Finance"
date: 2025-06-02 10:00:00 +0800
categories: [Computational Finance]
tags: [Probability Information Risk, Quantitative Finance, Path Integrals, Stochastic Calculus, Computational Finance]
math:       true        # enable KaTeX
---
# Notes on Quantitative Finance (Draft)

## Abstract
Resources in quantatitive finance are provided with short notes.  Emphasis is given to the empirical stylized facts obtained from statistical analysis of financial, economic and social data. Some history of the field is provided; including the influence of computation, applied mathematics, and theoretical physics over time. For completeness, the orthodox neoclassical view of asset pricing, portfolio theory, and risk is included. 
## 1 Time Series Analysis  

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
| S11 | [Marcaccioli & Livan*, *Stat-Mech Time Series* (2019)](https://arxiv.org/pdf/2003.12818) | Applies Boltzman statistical mechanics directly to time series. |
| S12 | [Ekapure et al, *Technical Analysis Meets Data Science* (2021)](https://arxiv.org/abs/2107.14695) | Applies machine learing directly to trend classification. |

---

## 2 Asset Pricing Theory

| ID | Source | Notes |
|---|---|---|
| S13 | [Tracy, *How to Read a Financial Report* (1999)](https://www.wiley.com/en-us/How+to+Read+a+Financial+Report%3A+Wringing+Vital+Signs+Out+of+the+Numbers%2C+10th+Edition-p-9781394268719) | Distils accounting statements into key cash-flow and leverage signals often engineered as factors in option-carry models. |
| S14 | [Cochrane, *Asset Pricing* (2000)](https://press.princeton.edu/books/hardcover/9780691121376/asset-pricing) | Derives the stochastic-discount-factor framework central to risk-neutral valuation. |
| S15 | [Duffie, *Dynamic Asset-Pricing Theory* (2001)](https://press.princeton.edu/books/hardcover/9780691090221/dynamic-asset-pricing-theory) | Itô-calculus proofs for optimal-exercise boundaries and contingent-claim valuation in continuous time. |
| S16 | [Bouchaud & Potters, *Theory of Financial Risk & Derivative Pricing* (2003)](https://www.cambridge.org/core/books/theory-of-financial-risk-and-derivative-pricing/5BBBA04CE72ED9E5E7C1C028D9A94FCB) | Integrates heavy-tailed return statistics into Black–Scholes-type PDEs via fractional diffusions. |
| S17 | [Voit  *Statistical Mechanics of Financial Markets* (2005)](https://link.springer.com/book/10.1007/b137351) | Statistical methods applied broadly to quantiative finance. |
| S18 | [Kleinert, *Path Integrals in Option Pricing* (2016)](https://arxiv.org/abs/1611.04320) | Pricing under alpha stable Levy processes. |
| S19 | [Rebonato, *Bond Pricing & Yield-Curve Modeling* (2018)](https://www.cambridge.org/core/books/bond-pricing-and-yield-curve-modeling/8BD16E2AC2B8CB6248A151F4BD5D25E8) | Presents PCA-driven term-structure dynamics. |


---

## 3 Financial Data: Stylized Facts   

| ID | Source | Notes |
|---|---|---|
| S20 | [Di Francesco *et al.*, *Random Matrices* (1994)](https://arxiv.org/abs/hep-th/9306153) | Random-matrix theory using physical models. |
| S21 | [Mantegna & Stanley, *Introduction to Econophysics* (2000)](https://www.cambridge.org/core/books/introduction-to-econophysics/6A2727FE42578790E6E1021B7955EE30) | Introductory text viewing financial data from the perspective of statistical physics. |
| S22 | [Mandelbrot, *The Misbehavior of Markets* (2004)](https://www.amazon.com/Misbehavior-Markets-annotated-Benoit-Mandelbrot/dp/B0077T2DIY) | Argues for fractal scaling and α-stable processes over Gaussian assumptions. |
| S23 | [Farmer et al, *Is Economics the Next Physical Science?* (2005)](https://pubs.aip.org/physicstoday/article-abstract/58/9/37/399433/Is-Economics-the-Next-Physical-Science-An-emerging?redirectedFrom=fulltext) | Advocates physicists’ universality concepts for financial innovation. |
| S24 | [Yakovenko, *Econophysics* (2008)](https://arxiv.org/abs/0709.3662) | Review of the literature and methods. |
| S25 | [Chakraborti *et al*, *Econophysics* (2010)](https://arxiv.org/abs/0909.1974) | Review of the literatute and methods. |
| S26 | [Chakrabarti *et al.*, *Econophysics* (2012)](https://www.jstor.org/stable/23251800) | Review of the literature and methods. |
| S27 | [Chakraborti *et al.*, *Econophysics* (2013)](https://link.springer.com/chapter/10.1007/978-3-319-08473-2_11) | Review of the literature and methods. |
| S28 | [Sornette, *Econophysics* (2014)](https://arxiv.org/abs/1404.0243) | Review of the literature and methods. |
| S29 | [Abergel et al, *Econophysics & Sociophysics* (2017)](https://link.springer.com/book/10.1007/978-3-319-47705-3) | Expansion to social networks, diffusion, and power laws. |
| S30 | [Schinkus, *A History of Econophysics* (2018)](https://www.repository.cam.ac.uk/items/61fb15c9-7e20-4229-9327-5213a3916356) | PhD disseration history and philosophy of science. Complex systems, Sante Fe Institute.  |
| S31 | [Sornette, *Multifractals in Finance* (2018)](https://arxiv.org/abs/1805.04750) | Deep dive into multifractal analysis of financial data. |
| S32 | [Bouchaud, *Econophysics* (2019)](https://arxiv.org/abs/1901.03691) | Review of the literature and methods. |
| S33 | [Abergel *et al.*, *Econophysics & Sociophysics* (2019)](https://link.springer.com/book/10.1007/978-3-030-11364-3) | Includes social networks, diffusion and dynamics. |
| S34 | [Potters & Bouchaud, *A First Course in Random-Matrix Theory* (2020)](https://www.cambridge.org/core/books/first-course-in-random-matrix-theory/2292A554A9BB9E2A4697C35BCE920304) | Foundations of RMT with applications to covariance of assets. |
| S35 | [Bouchaud et al, *Spin-Glass Markets* (2023)](https://arxiv.org/abs/2306.16165) | Spin glass methods (replica, replica symmetry breaking, cavity method) applied to generic complex data. |

---
## 4 Market Microstructures 

| ID | Source | Notes |
|---|---|---|
| S36 | [Farmer, *Slippage* (1996)](https://oms-inet.files.svdcdn.com/production/files/slippage.pdf) | Introduction to market-impact cost functions. |
| S37 | [Farmer *Market Ecology & Evolution* (1998)](https://arxiv.org/abs/adap-org/9812005) | Models trader populations with Lotka–Volterra dynamics to explain clustered volatility and intraday skew shifts. |
| S38 | [Pompian et al, *Behavioral Finance* (2006)](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119202400) | Catalogues cognitive biases that leak into demand‐pressure anomalies exploitable via volatility and skew trades. |
| S39 | [Abergel, *Limit Order Books* (2016)](https://www.cambridge.org/us/universitypress/subjects/mathematics/mathematical-finance/limit-order-books?format=HB&isbn=9781107163980) | Empirical order-book stylised facts aand agent based models. |
| S40 | [Lehalle & Laruelle, *Market Microstructure* (2018)](https://www.worldscientific.com/worldscibooks/10.1142/10739) | Calibrates Market impact, order-flow clustering, liquidity, regulation, and persistence. |
| S41 | [Bouchaud *et al.*, *Trades, Quotes & Prices* (2018)](https://www.cambridge.org/core/books/trades-quotes-and-prices/029A71078EE4C41C0D5D4574211AB1B5) | Market impact, order-flow, liquidity. |
| S42 | [Cont & Mueller, *SPDEs for Limit-Order Books* (2020)](https://arxiv.org/abs/1904.03058) | Introduces stochastic-PDE modeling of limit order books. |

---

## 5 Multi-Asset Structures and Factor Analysis  

| ID | Source | Notes |
|---|---|---|
| S43 | [Sethna, *Statistical Mechanics of Inference* (2017)](https://arxiv.org/abs/1503.06205) | Canonical sectors from unsupervised learning. |
| S44 | [Prigent, *Portfolio Optimization* (2007)](https://www.routledge.com/Portfolio-Optimization-and-Performance-Analysis/Prigent/p/book/9781584885788) | Presents quadratic-programming routines for mean-variance allocation with option and transaction-cost constraints. |
| S45 | [Peters, *Ergodicity & the Kelly Criterion* (2010)](https://arxiv.org/abs/0902.2965) | Justifies growth-optimal position sizing and leverage control for volatility-targeting strategies. |
| S46 | [Strachman, *Hedge-Fund Management* (2012)](https://www.wiley.com/en-us/The+Fundamentals+of+Hedge+Fund+Management%3A+How+to+Successfully+Launch+and+Operate+a+Hedge+Fund%2C+2nd+Edition-p-9781118239230) | Industry, regulation, structure, accounting, marketing, risk management. |
| S47 | [Joshi, *Mathematical Portfolio Theory* (2013)](https://www.cambridge.org/us/universitypress/subjects/mathematics/optimization-or-and-risk-analysis/introduction-mathematical-portfolio-theory?format=HB&isbn=9781107042315) | Neoclassical approach to efficient frontier. |
| S48 | [Rebonato & Denev, *Portfolio Management under Stress* (2013)](https://www.cambridge.org/core/books/portfolio-management-under-stress/481A8284865AAF4894011413D5E2D487) | Uses Bayesian networks for asset allocation. |
| S49 | [Bodie, Kane & Marcus, *Investments* (2018)](https://www.mheducation.com/highered/product/Investments-Bodie.html) | Neoclassical view including CAPM and APT. |
| S50 | [Brealey, Myers & Allen, *Principles of Corporate Finance* (2019)](https://www.mheducation.com/highered/product/Principles-of-Corporate-Finance-Brealey.html) | Neoclassical approach to corporate capital-budgeting decisions and project flexibilities. |
| S51 | [Baker & Filbeck, *Hedge Funds* (2021)](https://academic.oup.com/book/25365) | Performance, regulation, and factor replication techniques across global hedge-fund sector. |
| S52 | [Bardoscia *et al.*, *Financial Networks* (2021)](https://arxiv.org/abs/2103.05623) | Dynamical evolution of financial networks. |
| S53 | [Lopez de Prado, *Causal Factor Investing* (2023)](https://www.cambridge.org/core/elements/causal-factor-investing/9AFE270D7099B787B8FD4F4CBADE0C6E) | Systematization of factor analysis. |

---
## 6 Risk 

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
## 7 Complexity Economics   

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