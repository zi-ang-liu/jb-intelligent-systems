# Gradient Descent

最急降下法

$\mathbf{x} \in \mathbb{R}^n$の関数$f(\mathbf{x})$を最小化する問題を考える。ここで、$f$は微分可能であるとする。

最急降下法は、以下の式で与えられる更新式を繰り返すことで、$f$の極小値を求めるアルゴリズムである。

$$
\mathbf{x}^{(k+1)} = \mathbf{x}^{(k)} - \alpha \nabla f(\mathbf{x}^{(k)})
$$

ここで、$\nabla f(\mathbf{x})$は$f$の勾配を表し、$\alpha$はステップサイズを表す。

勾配$\nabla f(\mathbf{x})$は、以下のように定義される。

$$
\nabla f(\mathbf{x}) = \left[ \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \ldots, \frac{\partial f}{\partial x_n} \right]
$$

$\alpha$は、ステップサイズを表すハイパーパラメータであり、適切な値を選択することでアルゴリズムの収束性能を向上させることができる。

最急降下法は、勾配の逆方向に進むことで、関数$f$の極小値を探索するアルゴリズムである。

最急降下法の停止条件として、よく使われるのは以下の式である。

$\|\nabla f(\mathbf{x})\| < \text{tol}$

$\|\cdot\|$ はベクトルのノルムを表し、$\text{tol}$はあらかじめ与えられた許容誤差である。

## アルゴリズム

```{prf:algorithm} Gradient descent
:label: gradient-descent-algorithm

**Inputs:** function $f$, gradient $\nabla f$, initial guess $\mathbf{x}^{(0)}$, step size $\alpha$, tolerance $\text{tol}$   
**Output:** estimate of the minimum $\mathbf{x}$

1. Initialize $\mathbf{x} \leftarrow \mathbf{x}^{(0)}$
2. While $\|\nabla f(\mathbf{x})\| > \text{tol}$:
    1. $\mathbf{x} \leftarrow \mathbf{x} - \alpha \nabla f(\mathbf{x})$
3. Return $\mathbf{x}$
```

## Pythonによる実装

```python
import numpy as np

def gradient_descent(f, grad, x0, alpha=1e-3, tol=1e-6):
    """
    Gradient descent (optimization algorithm)

    Parameters
    ----------
    f : function
        The function to minimize
    grad : function
        The gradient of the function
    x0 : np.ndarray
        Initial guess
    alpha : float
        Step size
    tol : float
        Tolerance

    Returns
    -------
    x : np.ndarray
        The estimate of the minimum
    """
    x = x0
    while np.linalg.norm(grad(x)) > tol:
        x = x - alpha * grad(x)
    return x


def f(x):
    return x[0]**2 + x[1]**2

def grad(x):
    return np.array([2*x[0], 2*x[1]])

x0 = np.array([1.0, 1.0])
x = gradient_descent(f, grad, x0)
print(x)
```