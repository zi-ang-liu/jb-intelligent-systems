# ニュートン法

ニュートン法は数値解析において、求根アルゴリズムの１つです。

ニュートン法では、以下の漸化式を用いて解を求めます。

$$
x^{(k+1)} = x^{(k)} - \frac{f(x^{(k)})}{f'(x^{(k)})}
$$

$x^{(0)}$を与えられた初期値として、上記の漸化式を繰り返し適用することで、$x^{(1)}, x^{(2)}, \ldots$を求めます。

ニュートン法の停止条件として、よく使われるのは以下の２つです。

1. $|f(x^{(k)})| < \epsilon$
2. $|x^{(k+1)} - x^{(k)}| < \epsilon$

ここで、$\epsilon$はあらかじめ与えられた許容誤差です。

## アルゴリズム

```{prf:algorithm} Newton's method
:label: newton-algorithm

**Inputs:** function $f$, derivative of the function $f'$, initial guess $x^{(0)}$, tolerance $\epsilon$   
**Output:** estimate of the root $x$

1. $x \leftarrow x^{(0)}$
2. While $|f(x)| > \epsilon$:
    1. $x \leftarrow x - f(x) / f'(x)$
3. Return $x$
```

## 実装

```python
def newton(f, df, x0, tol=1e-6):
    """
    Newton's method: root finding algorithm

    Parameters
    ----------
    f : function
        The function to find the root of
    df : function
        The derivative of the function
    x0 : float
        Initial guess
    tol : float
        Tolerance

    Returns
    -------
    x : float
        The estimated root

    """

    x = x0
    while True:
        fx = f(x)
        dfx = df(x)

        if abs(fx) < tol:
            break

        if dfx == 0:
            raise ValueError("Derivative is zero. No solution found.")

        x = x - fx / dfx
    return x


def df(x):
    return 2 * x


def f(x):
    return x**2 - 4


x = newton(f, df, 3)
print(f"Root={x}")
```