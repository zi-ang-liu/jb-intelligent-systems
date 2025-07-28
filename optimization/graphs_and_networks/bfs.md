# Breadth-First Search

```{prf:algorithm} Breadth-First Search
:label: bfs-algorithm
**Input**: A graph $G = (V, E)$ and a source node $s$   
**Output**: The set of nodes reachable from $s$ 

1. $Q \leftarrow$ a FIFO queue, with node as an element
2. $Q.\text{enqueue}(s)$
3. $researched \leftarrow \{s\}$
4. **while** $Q \neq \emptyset$ **do**:
    1. $v \leftarrow Q.\text{dequeue}()$
    2. **if** $v$ is the goal **then return** $v$
    3. **for each** $v_i \in \mathcal{S}(v)$ **do**:
        1. **if** $v_i \notin researched$ **then**:
            1. $researched \leftarrow researched \cup \{v_i\}$
            2. $Q.\text{enqueue}(v_i)$
5. **return** failure
```
