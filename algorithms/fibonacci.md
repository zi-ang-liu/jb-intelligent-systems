# Fibonacci

## Algorithm

```{prf:algorithm} Fibonacci
:label: fibonacci-algorithm

**Inputs:** integer $n$
**Output:** integer $F(n)$

1. If $n = 0$:
    1. Return $0$
2. If $n = 1$:
    1. Return $1$
3. Else:
    1. $F(n) \leftarrow F(n-1) + F(n-2)$
    2. Return $F(n)$
```

```{prf:algorithm} Fibonacci memoization
:label: fibonacci-memoization-algorithm

**Inputs:** integer $n$, dictionary $memo$
**Output:** integer $F(n)$

1. If $n$ in $memo$:
    1. Return $memo[n]$
2. If $n = 0$:
    1. Return $0$
3. If $n = 1$:
    1. Return $1$
4. Else:
    1. $memo[n] \leftarrow F(n-1) + F(n-2)$
    2. Return $memo[n]$
```

## Implementation

```python
def fibonacci(n):
    """
    Calculate the nth Fibonacci number using recursion.

    Parameters
    ----------
    n : int
        The position in the Fibonacci sequence.

    Returns
    -------
    int
        The nth Fibonacci number.
    """
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

```python
def fibonacci_memoization(n, memo=None):
    """
    Calculate the nth Fibonacci number using memoization.

    Parameters
    ----------
    n : int
        The position in the Fibonacci sequence.
    memo : dict, optional
        A dictionary to store previously computed Fibonacci numbers.

    Returns
    -------
    int
        The nth Fibonacci number.
    """
    if memo is None:
        memo = {}
    
    if n in memo:
        return memo[n]
    
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        memo[n] = fibonacci_memoization(n - 1, memo) + fibonacci_memoization(n - 2, memo)
        return memo[n]
```
