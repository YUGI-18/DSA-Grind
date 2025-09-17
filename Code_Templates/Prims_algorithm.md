Perfect 👍 Let’s add **Prim’s Algorithm** in the same revision format: 
# 📌 Prim’s Algorithm (C++) – Minimum Spanning Tree (MST)

---

## 🔹 What is Prim’s Algorithm?

Prim’s Algorithm is a **greedy algorithm** used to find a **Minimum Spanning Tree (MST)** of a weighted, undirected graph.

* MST = A subset of edges that connects all vertices with **minimum total edge weight** and **no cycles**.
* Unlike Kruskal’s (which sorts edges), Prim’s **grows the MST node by node**.

---

## 🔹 Process (Step by Step)

1. Start with an **arbitrary node** (usually `0`).
2. Use a **priority queue (min-heap)** to always pick the **minimum weight edge** that connects a node in the MST to a node outside the MST.
3. Mark the chosen node as part of MST.
4. Repeat until all nodes are included.

---

## 🔹 Template Code (without main)

```cpp
#include <bits/stdc++.h>
using namespace std;

int primMST(int n, vector<vector<pair<int,int>>>& adj) {
    // n = number of vertices
    // adj[u] = {v, w} means edge u-v with weight w

    vector<int> key(n, INT_MAX);   // Minimum edge weight to include vertex
    vector<bool> inMST(n, false);  // Whether vertex is included in MST
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;

    int mstWeight = 0;
    key[0] = 0; // Start from node 0
    pq.push({0, 0}); // {weight, node}

    while (!pq.empty()) {
        int u = pq.top().second;
        int w = pq.top().first;
        pq.pop();

        if (inMST[u]) continue;
        inMST[u] = true;
        mstWeight += w;

        for (auto [v, weight] : adj[u]) {
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                pq.push({key[v], v});
            }
        }
    }

    return mstWeight; // total weight of MST
}
```

---

## 🔹 Complexity

* **Time Complexity:** `O(E log V)`

  * Each edge insertion/deletion in PQ → `O(log V)`.
* **Space Complexity:** `O(V)`

  * `key[]`, `inMST[]`, and priority queue.

---

## 🔹 When to Use Prim’s?

✅ Use Prim’s when:

* Graph is **dense** (many edges).
* You need MST for **adjacency list** representation.
* Works well with **priority queue**.

✅ Use Kruskal’s when:

* Graph is **sparse** (fewer edges).
* Easier to implement with **Disjoint Set (DSU/Union-Find)**.

---
