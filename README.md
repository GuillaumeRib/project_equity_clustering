# Equity Clustering — Unsupervised Learning on S&P 500 Returns

Clustering S&P 500 stocks on their return profiles, to see whether return-based
groupings match the GICS sector classification.

**[Read the full notebook with interactive charts →](https://guillaumerib.github.io/project_equity_clustering/)**

## Method

- S&P 500 tickers and GICS sectors scraped from Wikipedia; daily adjusted close
  prices from `yfinance` since 2015, resampled to weekly returns
- Random sample of 350 stocks; `StandardScaler` on the return matrix, then PCA
  with 20 components (~67% cumulative explained variance)
- K-Means on the PCA loadings, with k = 11 to match the number of GICS sectors
- Hierarchical clustering using Ward linkage on the covariance matrix
- Correlation heatmaps reordered by each method, and cluster composition by sector
- Appendix: silhouette and elbow methods to examine the optimal k

## Results

Clusters are evaluated on average within-cluster correlation (cohesion, higher is
better) and between-cluster correlation (separation, lower is better).

| Method        | Within-cluster | Between-cluster |
|---------------|----------------|-----------------|
| PCA + K-Means | 0.525          | 0.657           |
| Hierarchical  | 0.519          | 0.590           |
| GICS sectors  | 0.506          | 0.688           |

K-Means produces the most internally consistent clusters; hierarchical clustering
gives the clearest separation between them. Both improve on GICS sectors, which
score lowest on cohesion and highest on overlap — market-defined sectors do not
fully capture how stocks actually co-move.

## Stack

Python · pandas · numpy · scikit-learn · SciPy · yfinance · Plotly · seaborn · matplotlib

A K-Means version of this analysis is integrated into
[project_markets_dash](https://github.com/GuillaumeRib/project_markets_dash).
