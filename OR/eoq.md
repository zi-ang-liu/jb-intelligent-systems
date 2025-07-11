# The Economic Order Quantity Model

The *Economic Order Quantity* (EOQ) model is one of the most foundamental inventory models. 

## Problem Definition and Optimization

The EOQ model assumes that the demand rate $d$ over a year is deterministic and constant. The lead time is 0, that is, orders are received immediately. Every time an order is placed, a fixed cost $K$ is incurred. The holding cost per unit per year is $h$. 

The goal of the EOQ model is to find the optimal order quantity $Q^*$ that minimizes the total cost, denoted as $g(Q)$:

$$
g(Q) = \frac{Kd}{Q} + \frac{hQ}{2}
$$

The first term represents the ordering cost, where $d/Q$ is the number of orders placed per year. The second term represents the holding cost, where $Q/2$ is the average inventory held.

The first derivative of the cost function is given by:

$$
g'(Q) = -\frac{Kd}{Q^2} + \frac{h}{2}
$$

The second derivative is given by:

$$
g''(Q) = \frac{2Kd}{Q^3} > 0
$$

Clearly, the second derivative is positive, indicating that the function is convex. When $g'(Q) = 0$, we can find the optimal order quantity $Q^*$:

$$
Q^* = \sqrt{\frac{2Kd}{h}}
$$

The following theorem summarizes the results of the EOQ model.

````{prf:theorem} Economic Order Quantity
:label: eoq
The optimal order quantity $Q^*$ that minimizes the total cost in the EOQ model is given by:

$$
Q^* = \sqrt{\frac{2Kd}{h}}
$$

The total cost $g(Q)$ is given by:

$$
g(Q^*) = \sqrt{2Kdh}
$$

````

## Implementation


```python
def eoq(K, h, demand):
    """
    Calculate the Economic Order Quantity (EOQ) and the total cost.

    Parameters:
    K (float): Fixed cost per order
    h (float): Holding cost per unit per year
    demand (float): Demand rate (units per year)

    Returns:
    tuple: Optimal order quantity (Q*) and total cost (g(Q*))
    """
    Q_optimal = (2 * K * demand / h) ** 0.5
    total_cost = (2 * K * demand * h) ** 0.5
    return Q_optimal, total_cost


# Example usage
K = 8  # Fixed cost per order
h = 0.225  # Holding cost per unit per year
demand = 1300  # Demand rate (units per year)
optimal_order_quantity, total_cost = eoq(K, h, demand)
print(f"Optimal Order Quantity (Q*): {optimal_order_quantity}")
print(f"Total Cost (g(Q*)): {total_cost}")
```