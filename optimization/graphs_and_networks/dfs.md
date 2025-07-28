# Depth-First Search

```{prf:algorithm} Depth-First Search
:label: dfs-algorithm
**Input**: A graph $G = (V, E)$ and a source node $s$   
**Output**: The set of nodes reachable from $s$

1. $S \leftarrow$ a stack, with node $s$ as an element
2. $researched \leftarrow \{s\}$
3. **while** $S \neq \emptyset$ **do**:
    1. $v \leftarrow S.\text{pop}()$
    2. **if** $v$ is the goal **then return** $v$
    3. **for each** $v_i \in \mathcal{S}(v)$ **do**:
        1. **if** $v_i \notin researched$ **then**:
            1. $researched \leftarrow researched \cup \{v_i\}$
            2. $S.\text{push}(v_i)$
4. **return** failure
```
