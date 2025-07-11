# Data Envelopment Analysis

## Introduction

## Example

## CCR Model

The CCR model was introduced by Charnes, Cooper, and Rhodes in 1978. This is one of the most basic DEA models. 

### Notation

- $i$: index for input, $i = 1, \ldots, m$
- $r$: index for output, $r = 1, \ldots, s$
- $j$: index for DMU, $j = 1, \ldots, n$
- $x_{ij}$: amount of input $i$ used by DMU $j$
- $y_{rj}$: amount of output $r$ produced by DMU $j$
- $u_r$: weight for output $r$
- $v_i$: weight for input $i$

### Ratio Form

The CCR model can be expressed in the ratio form as follows:

$$
\begin{align*}
\max & \quad h_o(\mathbf{u}, \mathbf{v}) = \frac{\sum_{r} u_r y_{ro}}{\sum_{i} v_i x_{io}} \\
\text{s.t.} & \quad \frac{\sum_{r} u_r y_{rj}}{\sum_{i} v_i x_{ij}} \leq 1, \quad j = 1, \ldots, n \\
& \quad u_r \geq 0, \quad r = 1, \ldots, s \\
& \quad v_i \geq 0, \quad i = 1, \ldots, m
\end{align*}
$$

### "Charnes-Cooper" Transformation

The CCR model can be transformed into a linear programming problem by changing the decision variables from $\mathbf{u}$ and $\mathbf{v}$ to $\pmb{\mu}$ and $\pmb{\nu}$, respectively. The transformed model is as follows:

$$
\begin{align*}
\max & \quad z = \sum_{r=1}^{s} \mu_r y_{ro} \\
\text{s.t.} & \quad \sum_{r=1}^{s} \mu_r y_{rj} - \sum_{i=1}^{m} \nu_i x_{ij} \leq 0, \quad j = 1, \ldots, n \\
& \quad \sum_{i=1}^{m} \nu_i x_{io} = 1 \\
& \quad \mu_r \geq 0, \quad r = 1, \ldots, s \\
& \quad \nu_i \geq 0, \quad i = 1, \ldots, m
\end{align*}
$$

**Theorem 1**. The fractional program is equivalent to the linear program.

### Dual Problem


## References

1. W. W. Cooper, L. M. Seiford, and J. Zhu, Eds., Handbook on data envelopment analysis, 2nd ed. New York, NY: Springer, 2010.
2. W. W. Cooper, L. M. Seiford, and K. Tone, Data envelopment analysis: A comprehensive text with models, applications, references and DEA-solver software, 2nd ed. New York, NY: Springer, 2006.
  
## 

| English                         | Japanese   |
| ------------------------------- | ---------- |
| Data Envelopment Analysis (DEA) | 包絡分析法 |
| Decision Making Unit (DMU)      |            |
| Reference Set                   |            |
| Efficient                       |            |

