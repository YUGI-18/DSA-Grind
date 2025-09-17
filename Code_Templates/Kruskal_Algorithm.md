
# 📌 Kruskal’s Algorithm (C++) – Minimum Spanning Tree (MST)

---

## 🔹 What is Kruskal’s Algorithm?

Kruskal’s Algorithm is a **greedy algorithm** used to find a **Minimum Spanning Tree (MST)** of a weighted, undirected graph.

* MST = Subset of edges that connects all vertices with **minimum total edge weight** and **no cycles**.
* Unlike Prim’s (which grows MST node by node), **Kruskal’s sorts all edges by weight and picks the smallest valid edge** (no cycle).
* Requires **Disjoint Set Union (DSU / Union-Find)** to detect cycles efficiently.

---

## 🔹 Process (Step by Step)

1. Sort all edges in **non-decreasing order of weight**.
2. Initialize an empty MST.
3. For each edge `(u, v, w)` in sorted order:

   * If `u` and `v` are in different sets (no cycle), include this edge in MST and union them.
   * Else, skip the edge.
4. Continue until MST has `V-1` edges.

---

## 🔹 Template Code (without main)

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Edge {
    int u, v, w;
};

// Disjoint Set Union (Union-Find)
struct DSU {
    vector<int> parent, rank;

    DSU(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]); // path compression
        return parent[x];
    }

    bool unite(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false;
        if (rank[px] < rank[py]) swap(px, py);
        parent[py] = px;
        if (rank[px] == rank[py]) rank[px]++;
        return true;
    }
};

int kruskalMST(int n, vector<Edge>& edges) {
    sort(edges.begin(), edges.end(), [](Edge &a, Edge &b) {
        return a.w < b.w;
    });

    DSU dsu(n);
    int mstWeight = 0;
    int edgesUsed = 0;

    for (auto &e : edges) {
        if (dsu.unite(e.u, e.v)) {
            mstWeight += e.w;
            edgesUsed++;
            if (edgesUsed == n - 1) break;
        }
    }

    return mstWeight;
}
```

---

## 🔹 Complexity

* **Sorting edges:** `O(E log E)`
* **Union-Find operations:** `O(E α(V))` ≈ `O(E)` (where `α` = inverse Ackermann function, very small).
* **Total Time Complexity:** `O(E log E)`
* **Space Complexity:** `O(V)`

---

## 🔹 When to Use Kruskal’s?

✅ Use Kruskal’s when:

* Graph is **sparse** (few edges compared to vertices).
* Easier to implement with **edge list** representation.
* You already have edges given (instead of adjacency list).

✅ Use Prim’s when:

* Graph is **dense** (many edges).
* Better with **adjacency list** representation.

---
