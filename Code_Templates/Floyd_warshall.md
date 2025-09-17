
# 📌 Floyd–Warshall Algorithm (C++)

---

## 🔹 What is Floyd–Warshall?

The **Floyd–Warshall Algorithm** is an **all-pairs shortest path algorithm**.
It computes the shortest distances between **every pair of vertices** in a weighted graph.

* Works with **negative edge weights**.
* Detects **negative weight cycles**.
* Uses **Dynamic Programming**.

---

## 🔹 Process (Step by Step)

1. **Initialization**

   * Create a `dist[][]` matrix.
   * `dist[i][j] = weight of edge (i → j)` if exists, else `∞`.
   * `dist[i][i] = 0`.

2. **Relaxation (via intermediate nodes)**

   * For each vertex `k`, check if the path `i → k → j` is shorter than `i → j`.
   * Formula:

     ```
     dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
     ```

3. **Negative Cycle Check**

   * If `dist[i][i] < 0` for any `i`, then there’s a **negative weight cycle**.

---

## 🔹 Template Code (without main)

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> floydWarshall(int n, vector<vector<int>>& graph) {
    // graph[i][j] = weight of edge i->j, or INF if no edge
    vector<vector<int>> dist = graph;

    // Run Floyd–Warshall
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i][k] != INT_MAX && dist[k][j] != INT_MAX) {
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }

    // Detect negative weight cycle
    for (int i = 0; i < n; i++) {
        if (dist[i][i] < 0) {
            throw runtime_error("Graph contains a negative weight cycle!");
        }
    }

    return dist;
}
```

---

## 🔹 Complexity

* **Time Complexity:** `O(V³)`

  * Triple nested loop over `n` vertices.
* **Space Complexity:** `O(V²)`

  * Stores distance matrix.

---

## 🔹 When to Use Floyd–Warshall?

✅ Use Floyd–Warshall if:

* You need **shortest paths between all pairs of nodes**.
* The graph is **small/medium sized** (because `O(V³)` is expensive).
* The graph has **negative edges** but no negative cycles.

❌ Avoid for **very large graphs** → use **Dijkstra (per node)** instead.

---
