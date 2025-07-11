# Momentum

## Algorithm

```{prf:algorithm} Momentum
:label: momentum-algorithm

**Inputs:** function $f$, gradient $\nabla f$, initial guess $\mathbf{x}^{(0)}$, step size $\alpha$, momentum parameter $\beta$, tolerance $\text{tol}$   
**Output:** estimate of the minimum $\mathbf{x}$

1. Initialize $\mathbf{x} \leftarrow \mathbf{x}^{(0)}$
2. Initialize $\mathbf{v} \leftarrow \mathbf{0}$
3. While $\|\nabla f(\mathbf{x})\| > \text{tol}$:
    1. $\mathbf{v} \leftarrow \beta \mathbf{v} - \alpha \nabla f(\mathbf{x})$
    2. $\mathbf{x} \leftarrow \mathbf{x} + \mathbf{v}$
4. Return $\mathbf{x}$
```

## Python implementation

```python
import numpy as np

def momentum(f, grad, x0, alpha=1e-3, beta=0.9, tol=1e-6):
    """
    Momentum (optimization algorithm)

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
    beta : float
        Momentum parameter
    tol : float
        Tolerance

    Returns
    -------
    x : np.ndarray
        The estimate of the minimum
    """
    x = x0
    v = np.zeros_like(x)
    while np.linalg.norm(grad(x)) > tol:
        v = beta * v - alpha * grad(x)
        x = x + v
    return x


def f(x):
    return x[0]**2 + x[1]**2

def grad(x):
    return np.array([2*x[0], 2*x[1]])

x0 = np.array([1.0, 1.0])
x = momentum(f, grad, x0)
print(x)
```