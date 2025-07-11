# Analytic Hierarchy Process

## Real-world application

## Example



## Introduction




### Notation
- $\mathbf{A}$: pairwise comparison matrix
- $w_i$: importance of element $i$
- $a_{ij}$: ratio of the importance of element $i$ to element $j$

### Pairwise comparison matrix

The pairwise comparison matrix $\mathbf{A}$ is a square matrix of order $n$ with elements $a_{ij}$, where $a_{ij}$ is the ratio of the importance of element $i$ to element $j$. Formally, the pairwise comparison matrix is defined as follows:

$$
\mathbf{A} = \begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn} \\
\end{bmatrix}
$$

$a_{ij}$ is the ratio of the importance of element $i$ to element $j$. The elements of the matrix are defined as follows:

$$
a_{ij} = \frac{w_i}{w_j}
$$

where $w_i$ and $w_j$ are the importance of elements $i$ and $j$, respectively. Then, the matrix $\mathbf{A}$ can be expressed as follows:

$$
\mathbf{A} = \begin{bmatrix}
w_1/w_1 & w_1/w_2 & \cdots & w_1/w_n \\
w_2/w_1 & w_2/w_2 & \cdots & w_2/w_n \\
\vdots & \vdots & \ddots & \vdots \\
w_n/w_1 & w_n/w_2 & \cdots & w_n/w_n \\
\end{bmatrix}
$$

There are two important properties of the pairwise comparison matrix $\mathbf{A}$:

- If $a_{ij} = a$, then $a_{ji} = 1/a$.
- $a_{ij} a_{jk} = a_{ik}$.

### Importance scale

**Table: The fundamental scale of absolute numbers (Saaty, 2008)**

| Importance | Definition        | Explanation                                                                      |
| ---------- | ----------------- | -------------------------------------------------------------------------------- |
| 1          | Equal             | Two activities contribute equally to the objective                               |
| 2          | Weak or slight    | -                                                                                |
| 3          | Moderate          | Experience and judgment slightly favor one activity over another                 |
| 4          | Moderate plus     | -                                                                                |
| 5          | Strong            | Experience and judgment strongly favor one activity over another                 |
| 6          | Strong plus       | -                                                                                |
| 7          | Very strong       | An activity is favored very strongly over another activity                       |
| 8          | Very, very strong | -                                                                                |
| 9          | Extreme           | The evidence favoring one activity over another is of the highest possible order |

### Eigenvector method

Let $\mathbf{w} = [w_1, w_2, \ldots, w_n]^T$ be the vector of the importance of elements. Then, the following equation holds:

$$
\mathbf{A} \mathbf{w} = 
\begin{bmatrix}
w_1/w_1 & w_1/w_2 & \cdots & w_1/w_n \\
w_2/w_1 & w_2/w_2 & \cdots & w_2/w_n \\
\vdots & \vdots & \ddots & \vdots \\
w_n/w_1 & w_n/w_2 & \cdots & w_n/w_n \\
\end{bmatrix}
\begin{bmatrix}
w_1 \\
w_2 \\
\vdots \\
w_n \\
\end{bmatrix}
= n 
\begin{bmatrix}
w_1 \\
w_2 \\
\vdots \\
w_n \\
\end{bmatrix}
= n \mathbf{w}
$$

Therefore, given the pairwise comparison matrix $\mathbf{A}$, the vector of the importance of elements $\mathbf{w}$ can be obtained by solving the following equation:

$$
\mathbf{A} \mathbf{w} = n \mathbf{w}
$$

In other words, $\mathbf{A} \mathbf{w} = n \mathbf{w}$ implies that the vector of the importance of elements $\mathbf{w}$ is an eigenvector of the matrix $\mathbf{A}$ with eigenvalue $n$. This equation can be rewritten as $(\mathbf{A} - n \mathbf{I}) \mathbf{w} = \mathbf{0}$, where $\mathbf{I} \in \mathbb{R}^{n \times n}$ is the identity matrix.

### Geometric mean method

$w_i$ is obtained as the geometric mean of the elements in the $i$-th row of the pairwise comparison matrix $\mathbf{A}$ divided by a normalization term so that the $\sum_{i} w_i = 1$.

$$
w_i = \frac{\left( \prod_{j=1}^{n} a_{ij} \right)^{1/n}}{\sum_{i=1}^{n} \left( \prod_{j=1}^{n} a_{ij} \right)^{1/n}}
$$

### Least squares method

$$
\begin{align*}
\min & \quad \sum_{i} \sum_{j} (a_{ij} - w_i/w_j)^2 \\
\text{s.t.} & \quad \sum_{i} w_i = 1
\end{align*}
$$

Local minimum.

### Normalized columns method

1. Normalize the columns of the pairwise comparison matrix $\mathbf{A}$ so that the sum of the elements in each column is 1.
2. Calculate the arithmetic mean of the elements in each row.
3. Normalize the vector of the arithmetic means so that the sum of the elements is 1.

Lack solid theoretical foundation.

## References

1. T. Saaty, “Decision making with the Analytic Hierarchy Process,” International Journal of Services Sciences, vol. 1, no. 1, pp. 83-98, Mar. 2008.
2. G. Crawford and C. Williams, “A note on the analysis of subjective judgment matrices,” J. Math. Psychol., vol. 29, no. 4, pp. 387–405, Dec. 1985.
  

  


##

| English                               | Japanese     |
| ------------------------------------- | ------------ |
| multi-criteria decision making (MCDM) |              |
| Analytic Hierarchy Process (AHP)      | 階層分析法   |
| Consistency index                     | 整合度       |
| pairwise comparison matrix            | 一対比較行列 |
