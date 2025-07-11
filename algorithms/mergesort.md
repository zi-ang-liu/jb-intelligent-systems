# Merge Sort

Merge sort is an efficient sorting algorithm. It was invented by John von Neumann in 1945.

## Algorithm

```{prf:algorithm} Merge 
:label: merge-algorithm

**Inputs:** sorted array $A$, sorted array $B$
**Output:** sorted array $C$

1. $i \leftarrow 1$
2. $j \leftarrow 1$
3. $C \leftarrow []$
4. While $i \leq \text{length}(A)$ and $j \leq \text{length}(B)$:
    1. If $A[i] < B[j]$:
        1. Append $A[i]$ to $C$
        2. $i \leftarrow i + 1$
    2. Else:
        1. Append $B[j]$ to $C$
        2. $j \leftarrow j + 1$
5. While $i \leq \text{length}(A)$:
    1. Append $A[i]$ to $C$
    2. $i \leftarrow i + 1$
 6. While $j \leq \text{length}(B)$:
    1. Append $B[j]$ to $C$
    2. $j \leftarrow j + 1$
6. Return $C$

```

```{prf:algorithm} Merge Sort
:label: merge-sort-algorithm

**Inputs:** array $A$
**Output:** sorted array $A$

1. $n \leftarrow \text{length}(A)$
2. If $n = 1$:
    1. Return $A$
3. Else:
    1. $m \leftarrow n / 2$
    2. $L \leftarrow A[1:m]$
    3. $R \leftarrow A[m+1:n]$
    4. $L \leftarrow \text{MergeSort}(L)$
    5. $R \leftarrow \text{MergeSort}(R)$
    6. $A \leftarrow \text{Merge}(L, R)$
    7. Return $A$
```

## Implementation

```python
def merge(left, right):
    """
    Merge two sorted arrays into one sorted array.

    Parameters
    ----------
    left : list
        The first sorted array
    right : list
        The second sorted array

    Returns
    -------
    list
        The merged sorted array
    """
    merged = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1

    merged.extend(left[i:])
    merged.extend(right[j:])

    return merged


def merge_sort(arr):
    """
    Merge sort algorithm.

    Parameters
    ----------
    arr : list
        The array to be sorted

    Returns
    -------
    list
        The sorted array
    """

    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)


if __name__ == "__main__":
    # Example usage
    arr = [38, 27, 43, 3, 9, 82, 10]
    sorted_arr = merge_sort(arr)
    print("Sorted array:", sorted_arr)
    # Output: Sorted array: [3, 9, 10, 27, 38, 43, 82]
```



    