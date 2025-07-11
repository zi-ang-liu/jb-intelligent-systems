# Bayesian Optimization

[A Tutorial on Bayesian Optimization](https://arxiv.org/abs/1807.02811) gives a good overview of the topic.

Bayesian Optimization is a powerful method for optimizing expensive objective functions. It builds a surrogate model using a machine learning model (often a Gaussian Process) to approximate the objective function, and uses an acquisition function to decide where to sample next. 

This method aims to optimize the following problem:

$$
\min_{\mathbf{x} \in \mathcal{X}} f(\mathbf{x})
$$

where $f: \mathcal{X} \to \mathbb{R}$ is the objective function, $\mathcal{X}$ is the solution space, and $f$ is an expensive function to evaluate.

## Algorithm

Let $\mathcal{D}_t = \{(x_i, y_i)\}_{i=1}^n$ be the data points collected at iteration $t$, where $\mathbf{x}_i \in \mathcal{X}$ is the input and $y_i = f(x_i)$ is the output of the objective function $f$. 

```{prf:algorithm} Bayesian Optimization
:label: BO

**Input**: Objective function $f$, initial data points $\mathcal{D}_0 = \{(\mathbf{x}_i, y_i)\}_{i=1}^n$, acquisition function $\alpha$, surrogate model $\hat{f}$, maximum budget $T$.   

1. $t \gets 0$
2. **while** $t < T$:
   1. update the surrogate model $\hat{f}$ using $\mathcal{D}_t$;
   2. $\mathbf{x}_{t+1} \gets \arg\max_{\mathbf{x} \in \mathcal{X}} a(\hat{f}, \mathbf{x})$;
   3. $y_{t+1} \gets f(\mathbf{x}_{t+1})$;
   4. $\mathcal{D}_{t+1} \gets \mathcal{D}_t \cup \{(\mathbf{x}_{t+1}, y_{t+1})\}$;
   5. $t \gets t + 1$;
3. **return** the best solution found in $\mathcal{D}_T$.
```

## Acquisition Functions

### Lower Confidence Bound (LCB)

Let $\hat{u}(\mathbf{x})$ be the predicted mean and $\hat{\sigma}(\mathbf{x})$ be the predicted standard deviation of the surrogate model at point $\mathbf{x}$. The LCB acquisition function is defined as:

$$
\alpha_{\text{LCB}}(\mathbf{x}) = \hat{u}(\mathbf{x}) - k \hat{\sigma} (\mathbf{x})
$$

where $k$ is a parameter that controls the trade-off between exploration and exploitation.

## Python Implementation

```python
import numpy as np
from scipy.optimize import minimize
from sklearn.gaussian_process import GaussianProcessRegressor


class BayesianOptimization:
    def __init__(
        self, objective_function, bounds, n_initial_points=10, n_iterations=20, n_dim=1
    ):
        self.objective_function = objective_function
        self.bounds = bounds
        self.n_initial_points = n_initial_points
        self.n_iterations = n_iterations
        self.n_dim = n_dim

    def initialize(self):
        self.data_X = np.random.uniform(
            self.bounds[0], self.bounds[1], (self.n_initial_points, self.n_dim)
        )
        self.data_y = [self.objective_function(x) for x in self.data_X]

    def fit_surrogate_model(self):
        self.gp = GaussianProcessRegressor()
        self.gp.fit(np.array(self.data_X), np.array(self.data_y))

    def acquisition_function(self, x):
        x = np.array(x).reshape(1, -1)
        mean, std = self.gp.predict(x, return_std=True)
        return mean - 1.96 * std

    def optimize(self):
        self.initialize()
        for _ in range(self.n_iterations):
            self.fit_surrogate_model()
            x0 = np.random.uniform(self.bounds[0], self.bounds[1], self.n_dim)
            bounds = list(zip(self.bounds[0], self.bounds[1]))
            res = minimize(
                fun=lambda x: self.acquisition_function(x),
                x0=x0,
                bounds=bounds,
            )
            x_next = res.x
            y_next = self.objective_function(x_next)
            self.data_X = np.append(self.data_X, [x_next], axis=0)
            self.data_y.append(y_next)
            print(f"Next point: {x_next}, Objective value: {y_next}")
        best_index = np.argmin(self.data_y)
        best_x = self.data_X[best_index]
        best_y = self.data_y[best_index]
        return best_x, best_y


class Sphere:
    def __init__(self, n_dim=10):
        self.n_dim = n_dim
        self.ub = np.ones(n_dim) * 5
        self.lb = -np.ones(n_dim) * 5

    def evaluate(self, x):
        return np.sum(x**2)


if __name__ == "__main__":

    func = Sphere(n_dim=2)

    bo = BayesianOptimization(
        objective_function=func.evaluate,
        bounds=(func.lb, func.ub),
        n_initial_points=50,
        n_iterations=100,
        n_dim=func.n_dim,
    )
    best_x, best_y = bo.optimize()
    print(f"Best x: {best_x}, Best y: {best_y}")
```