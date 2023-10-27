# Robust PCA Implementation

This repository provides an implementation of the Principal Component Pursuit by Alternating Directions (PCA-AD) algorithm as described in the paper [Principal Component Pursuit by Alternating Directions](https://arxiv.org/abs/0912.3599), with a focus on its application in electricity price analysis. The PCA-AD algorithm is used to separate a given matrix into a low-rank component and a sparse component, making it particularly suitable for addressing intermittent price spikes in electricity market data.

## Background

Electricity prices often exhibit smooth variations driven by supply and demand, but they can also experience abrupt price spikes that deviate significantly from the regular behavior. To better understand and handle these price spikes, we model the price data as a combination of two components:

- **Low-Rank Component (L)**: This represents the normal daily market behavior, characterized by smooth price variations.
- **Sparse Component (S)**: This captures the intermittent price spikes that deviate from the regular behavior.

We can express the price data matrix $M$ as the sum of these components:

$M = L + S$

The goal is to estimate both the low-rank component $L$ and the sparse component $S$ by solving the Robust Principal Component Analysis (RPCA) problem, formulated as:

$\min{\|L\|_* + \lambda |S|_1}$

subject to $L + S = M$

## Dataset

In this implementation, we use a dataset of electricity prices, which can be loaded from a CSV file. The dataset is transformed into a matrix $M$, where each row corresponds to a day, and each column corresponds to an hour. Visualizing this dataset helps us identify and separate the intermittent price spikes.

```python
import pandas as pd
from matplotlib import pyplot as plt

# Load the dataset from "Question1.csv"
data = pd.read_csv("Question1.csv", index_col=0, parse_dates=True)

# Unroll the daily values to plot the time series, revealing the spikes we aim to separate.
timeseries = data.stack()
timeseries.index = timeseries.index.droplevel(1)
timeseries.plot()

M = data.values
print(M.shape)  # The matrix M is 244 rows (days) by 24 columns (hours).
```

## Implementation

To solve for $L$ and $S$, the low-rank and sparse components of the matrix $M$, we implement the PCA-AD algorithm. The key components of the implementation are as follows:

- Singular Value Decomposition (SVD) is used to perform matrix factorization.
- Helper functions are defined for matrix shrinkage and soft thresholding.
- Algorithm parameters, such as $\mu$ and $\lambda$, are set.
- The main algorithm iteratively computes $L$ and $S$.
- Convergence is checked using a specified tolerance.

```python
import numpy as np
from numpy.linalg import svd

# Define helper functions (svd_shrink, shrink, soft_threshold)

# Set parameter values (mu, lam, max_iter, tol)

# Initialize variables (L, S, Y)

# Implement the algorithm

# Return the results (L, S)
```

## Results

The results of the robust PCA are visualized to show the separated low-rank component ($L$) and sparse component ($S). This provides insights into the underlying regular behavior and the intermittent spikes in the electricity price data.

```python
plt.plot(L.flatten())  # Plot the low-rank component
plt.plot(S.flatten())  # Plot the sparse component
```

This implementation allows you to apply the PCA-AD algorithm to analyze and separate components in electricity price data, which can be valuable for understanding and predicting price spikes in the market.

Please refer to the provided code and the referenced paper for a detailed understanding of the algorithm and its application.
