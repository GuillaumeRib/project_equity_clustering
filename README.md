# Equity Clustering — Unsupervised Learning on S&P 500 Returns

Clustering S&P 500 stocks on their return profiles, to see whether return-based
groupings match the GICS sector classification.

## Method

- S&P 500 tickers and GICS sectors scraped from Wikipedia; daily adjusted close
  prices from `yfinance`; weekly returns on a random sample of 350 stocks
- `StandardScaler` on the return matrix, then PCA with 20 components
  (~67% cumulative explained variance)
- K-Means on the PCA loadings — 11 clusters, selected by elbow and silhouette
- Hierarchical clustering (HCA) on covariance linkage, with dendrogram
- GICS sectors used as the baseline

## Results

Clusters are evaluated on average within-cluster correlation (cohesion, higher is
better) and between-cluster correlation (separation, lower is better).

| Method        | Within-cluster | Between-cluster |
|---------------|----------------|-----------------|
| PCA + K-Means | 0.525          | 0.657           |
| Hierarchical  | 0.519          | 0.590           |
| GICS sectors  | 0.506          | 0.688           |

K-Means produces the most internally consistent clusters; HCA gives the clearest
separation between them. Both improve on GICS sectors, which score lowest on
cohesion and highest on overlap — market-defined sectors do not fully capture
how stocks actually co-move.

## Stack

Python · pandas · numpy · scikit-learn · SciPy · yfinance · Plotly · seaborn · matplotlib

A K-Means version of this analysis is integrated into
[project_markets_dash](https://github.com/GuillaumeRib/project_markets_dash).

