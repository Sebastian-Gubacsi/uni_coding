# CP 312 Assignment 4 Solutions

## Question 1: Longest Exponential Subsequence [10 marks]

### (a) Subproblem Definition

Let `L[i]` denote the length of the longest exponential subsequence ending at position `i` with element `a[i]`.

### (b) Recurrence Rule

```
L[i] = 1 + max{L[j] : 1 ≤ j < i and a[i] ≥ 2 * a[j]}
```

If no such `j` exists, then `L[i] = 1`.

**Justification:** To extend an exponential subsequence to position `i`, we must append `a[i]` to a subsequence ending at some `j < i` where `a[i] ≥ 2 * a[j]`. We choose the `j` with maximum `L[j]` to maximize the length.

### (c) Pseudocode

```
LONGEST_EXPONENTIAL_SUBSEQUENCE(a, n)
    // Initialize arrays
    L[1..n] ← array of length n, all elements = 1
    prev[1..n] ← array of length n, all elements = -1
    
    // Fill the DP table
    for i = 2 to n do
        for j = 1 to i-1 do
            if a[i] ≥ 2 * a[j] then
                if L[j] + 1 > L[i] then
                    L[i] = L[j] + 1
                    prev[i] = j
    
    // Find the position with maximum length
    maxLength = 0
    maxIndex = -1
    for i = 1 to n do
        if L[i] > maxLength then
            maxLength = L[i]
            maxIndex = i
    
    // Reconstruct the subsequence
    subsequence = empty list
    current = maxIndex
    while current ≠ -1 do
        prepend a[current] to subsequence
        current = prev[current]
    
    return (maxLength, subsequence)
```

**Output Format:**
```
length: maxLength
subsequence: elements in subsequence
```

### (d) Time Complexity Analysis

**Analysis:**
- The outer loop runs `n` times (from `i = 2` to `n`)
- The inner loop runs at most `i-1` times for each `i`
- Total comparisons: `1 + 2 + 3 + ... + (n-1) = O(n²)`
- Finding the maximum length: `O(n)`
- Reconstructing the subsequence: `O(n)` in the worst case

**Total Time Complexity: O(n²)**

**Space Complexity: O(n)** for storing the `L` and `prev` arrays.

---

## Question 2: Two Knapsacks Problem [7 marks]

### Subproblem Definition

**Subproblem:** `DP[i][w1][w2]` = maximum total value achievable using items `1` to `i`, where the total weight in knapsack 1 is at most `w1` and the total weight in knapsack 2 is at most `w2`.

### Recurrence Rule

For each item `i`, we have three choices:
1. Place it in knapsack 1 (if it fits)
2. Place it in knapsack 2 (if it fits)
3. Don't include it in either knapsack

```
DP[i][w1][w2] = max {
    DP[i-1][w1][w2],                                    // Don't take item i
    DP[i-1][w1 - w(i)][w2] + v1(i)    if w(i) ≤ w1,   // Put in knapsack 1
    DP[i-1][w1][w2 - w(i)] + v2(i)    if w(i) ≤ w2    // Put in knapsack 2
}
```

**Base Case:** `DP[0][w1][w2] = 0` for all valid `w1` and `w2` (no items means zero value).

### Algorithm

```
TWO_KNAPSACKS(n, W1, W2, w[], v1[], v2[])
    // Initialize DP table
    DP[0..n][0..W1][0..W2] ← all elements = 0
    
    // Fill the DP table
    for i = 1 to n do
        for w1 = 0 to W1 do
            for w2 = 0 to W2 do
                // Option 1: Don't take item i
                DP[i][w1][w2] = DP[i-1][w1][w2]
                
                // Option 2: Put item i in knapsack 1
                if w(i) ≤ w1 then
                    DP[i][w1][w2] = max(DP[i][w1][w2], 
                                        DP[i-1][w1 - w(i)][w2] + v1(i))
                
                // Option 3: Put item i in knapsack 2
                if w(i) ≤ w2 then
                    DP[i][w1][w2] = max(DP[i][w1][w2], 
                                        DP[i-1][w1][w2 - w(i)] + v2(i))
    
    return DP[n][W1][W2]
```

### Order of Solving Subproblems

We solve subproblems in order of increasing `i` (item index), and for each `i`, we iterate through all possible weight combinations `(w1, w2)`.

### Correctness Justification

The algorithm is correct because:
1. We consider all possible placements for each item (knapsack 1, knapsack 2, or neither)
2. Each subproblem `DP[i][w1][w2]` depends only on subproblems with fewer items (`i-1`)
3. The optimal solution for `i` items is built from optimal solutions for `i-1` items
4. The recurrence correctly captures the constraint that items must be disjoint between knapsacks

### Time Complexity Analysis

- Three nested loops: `i` from 1 to `n`, `w1` from 0 to `W1`, `w2` from 0 to `W2`
- Each iteration performs constant work
- **Time Complexity: O(n · W1 · W2)**
- **Space Complexity: O(n · W1 · W2)** (can be optimized to O(W1 · W2) using rolling array)

### Polynomial Time Analysis

**This is NOT a polynomial-time algorithm** in the strict sense because:
- The running time is polynomial in `n`, `W1`, and `W2`
- However, `W1` and `W2` are numerical values, not the input size
- The input size for representing `W1` is `O(log W1)` bits
- The algorithm is **pseudo-polynomial** (polynomial in the numerical value of input, not input size)
- This is a weakly NP-hard problem

---

## Question 3: Graph Diameter [7 marks]

### Algorithm

The diameter is the maximum distance between any pair of vertices. We can compute it by running BFS from every vertex and finding the maximum distance encountered.

```
GRAPH_DIAMETER(G = (V, E))
    diameter = 0
    
    for each vertex u in V do
        // Run BFS from u
        dist[v] = ∞ for all v in V
        dist[u] = 0
        queue = empty queue
        enqueue(queue, u)
        maxDistFromU = 0
        
        while queue is not empty do
            v = dequeue(queue)
            for each neighbor w of v do
                if dist[w] = ∞ then
                    dist[w] = dist[v] + 1
                    maxDistFromU = max(maxDistFromU, dist[w])
                    enqueue(queue, w)
        
        diameter = max(diameter, maxDistFromU)
    
    return diameter
```

### Correctness Justification

**Correctness:**
1. BFS from a vertex `u` correctly computes the shortest path distance from `u` to all reachable vertices
2. The maximum distance found during BFS from `u` is the farthest vertex from `u`
3. By running BFS from every vertex, we find the maximum distance between any pair of vertices
4. Since the graph is connected, every vertex is reachable from every other vertex
5. The diameter is correctly computed as the maximum over all these distances

### Time Complexity

- BFS from a single vertex takes `O(|V| + |E|)` time
- We run BFS from all `|V|` vertices
- **Total Time Complexity: O(|V| · (|V| + |E|)) = O(|V|² + |V| · |E|)**

For sparse graphs where `|E| = O(|V|)`, this is `O(|V|²)`.
For dense graphs where `|E| = O(|V|²)`, this is `O(|V|³)`.

**Space Complexity: O(|V| + |E|)** for storing the graph and auxiliary arrays.

---

## Question 4: Tree Diameter using Divide and Conquer [6 marks]

### Algorithm

For a binary tree, the diameter can be computed recursively. For each node, the diameter either:
1. Passes through the root (longest path from left subtree through root to right subtree)
2. Is entirely in the left subtree
3. Is entirely in the right subtree

```
TREE_DIAMETER(root)
    if root = NULL then
        return 0
    
    result = computeDiameterAndHeight(root)
    return result.diameter

computeDiameterAndHeight(node)
    // Returns a structure containing diameter and height
    if node = NULL then
        return {diameter: 0, height: 0}
    
    // Recursively compute for left and right subtrees
    left = computeDiameterAndHeight(node.left)
    right = computeDiameterAndHeight(node.right)
    
    // Height of current node
    height = 1 + max(left.height, right.height)
    
    // Diameter is the maximum of:
    // 1. Diameter of left subtree
    // 2. Diameter of right subtree
    // 3. Longest path through current node (left.height + right.height)
    diameter = max(left.diameter, 
                   right.diameter, 
                   left.height + right.height)
    
    return {diameter: diameter, height: height}
```

### Correctness Justification

**Correctness:**
1. **Base case:** Empty tree has diameter 0
2. **Recursive case:** For any node, the diameter is either:
   - In the left subtree (handled by recursive call)
   - In the right subtree (handled by recursive call)
   - Passes through the current node (computed as sum of heights)
3. The height of each subtree gives us the longest path from that subtree to its root
4. Adding the heights of left and right subtrees gives the longest path through the current node
5. We take the maximum of all three possibilities

### Time Complexity

- Each node is visited exactly once
- At each node, we perform constant-time operations
- **Time Complexity: O(n)** where `n = |V|` is the number of nodes in the tree

**Space Complexity: O(h)** where `h` is the height of the tree (due to recursion stack)
- Best case (balanced tree): `O(log n)`
- Worst case (skewed tree): `O(n)`

### Comparison with Question 3

**Yes, this algorithm is asymptotically faster than the algorithm in Question 3.**

- Question 3 (general graph): `O(|V|² + |V| · |E|)`
- Question 4 (binary tree): `O(n)` where `n = |V|`

For a tree, `|E| = |V| - 1 = O(|V|)`, so Question 3's algorithm would be `O(|V|²)` for trees.

The divide-and-conquer approach is faster because:
1. It exploits the tree structure (no cycles)
2. Each node is visited only once instead of being the source of a BFS
3. We compute the diameter in a single traversal using the recursive structure

**Speedup factor: O(|V|) vs O(|V|²)** - a factor of `|V|` improvement!