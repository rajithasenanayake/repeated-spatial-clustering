# Introduction

Nearby locations in space often exhibit strong spatial relationships. Due to this, for spatial clusters to be meaninful, they are often required to be spatially contiguous. Similar spatial patterns can also emerge at distant locations in space as patches (not in proximity), which are referred to as repeated spatial clusters.

An ideal spatial clustering framework:
- Should form spatially contiguous clusters.
- Should identify repeated spatial clusters.

<div style="text-align: center;">
  <img src="images/Plot1.png" width="500" alt="Spatial Clusters">
  <p style="margin-top: 10px; font-style: italic;">Figure 1: Median house prices in Boston city</p>
</div>

Figure 1 shows that suburbs in Q4 creates spatiallly conitguous clusters. There are also a few suburbs belonging to Q4 that appear at distant locations resembling repeated spatial clusters.

There are various clustering algorithms used in spatial clustering, but they have thier own challenges.

Clustering algorithms that only use attributes (including spatial attributes) result in non-contiguous clusters:
1. K-Means Clustering.
2. Hierarchical Clustering.

Regionalization clustering ensures spatially cohesive clusters but does not identify repeated spatial patterns:
1. Density Based Spatial Clustering of Application with Noise (DBSCAN).
2. Constrained Hierarchical Clustering.


# Methods

The data we work on this project:
- \\(\textit{\textbf{X}}(s) \in \mathbb{R}^{n \times p}\\)
- \\(s \in \mathcal{D} \subset \mathbb{R}^{d}, d = 2\\)

The primary objective of this project is to develop a framework for identifying repeated spatial clusters while accounting for spatial dependence and contiguity. This is achieved by:
1. Identifying spatially contiguous clusters (Constrained Agglomerative Hierarchical Clustering is used for this step).
2. Perform a nonparametric spatial invariance test to identify repeated spatial patterns.
3. Re-partition the clusters based on the spatial invariance test results.

### Constrained Agglomerative Hierarchical Clustering

This is an extension of the standard agglomerative hierarchical clustering, where we can define contiguity constraints to guide the clustering process. Consider the follwing toy example shown in Figure 2.

<div style="text-align: center;">
  <img src="images/Plot2.png" width="250" alt="Toy Example">
  <p style="margin-top: 10px; font-style: italic; text-align: left;">Figure 2: X(1)=10, X(2)=20, X(3)=15, X(4)=12 with spatial locations 1, 2, 3, 4. The "must-links" created by the 2-nearest neighborhood structure are presented as edges.</p>
</div>

$$\begin{table}[ht]
\centering
\caption{Initial step: distance and links.}
\label{int_stp}
\begin{minipage}{0.3\textwidth}
    \centering
    \subcaption{Distance}{}
    \label{tab:distance}
    \begin{tabular}{@{} c r r r @{}} % Adjust columns as needed
        \toprule
         & 1 & 2 & 3 \\
        \midrule
        2 & 10 \\
        3 & 5 & 5 \\
        4 & 2 & 8 & 3 \\
        \bottomrule
    \end{tabular}
\end{minipage} \hspace{0.05\textwidth} % Adjust space between tables
\begin{minipage}{0.3\textwidth}
    \centering
    \subcaption{Links}{}
    \label{tab:links}
    \begin{tabular}{@{} c c c @{}} % Adjust columns as needed
        \toprule
        From & To & Dissimilarity \\
        \midrule
        1 & 2 & 10\\
        1 & 3 & 5\\
        2 & 3 & 5\\
        2 & 4 & 8\\
        3 & 4 & 3\\
        \bottomrule
    \end{tabular}
\end{minipage}
\end{table}$$
