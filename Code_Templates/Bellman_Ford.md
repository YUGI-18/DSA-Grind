
# 📌 Bellman–Ford Algorithm (C++)

---

## 🔹 What is Bellman–Ford?

Bellman–Ford is a **shortest path algorithm** that works on graphs with **negative weight edges** (but **no negative weight cycles** reachable from the source).

Unlike Dijkstra, which uses a greedy approach, Bellman–Ford uses **relaxation** repeatedly to guarantee the shortest paths.

---

## 🔹 Process (Step by Step)

1. **Initialization**

   * Distance of source = 0
   * Distance of all other vertices = ∞

2. **Relaxation (V-1 times)**

   * For each edge `(u, v, w)` → if `dist[u] + w < dist[v]`, update `dist[v] = dist[u] + w`.
   * Do this for all edges, repeat `V-1` times (because the shortest path in a graph of `V` vertices has at most `V-1` edges).

3. **Negative Cycle Check**

   * Do one more relaxation over all edges.
   * If any distance can still be reduced, then the graph contains a **negative weight cycle**.

---

## 🔹 Template Code

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Edge {
    int u, v, w;
};

vector<int> bellmanFord(int n, vector<Edge>& edges, int src) {
    vector<int> dist(n, INT_MAX);
    dist[src] = 0;

    // Step 1: Relax edges (V-1) times
    for (int i = 1; i <= n - 1; i++) {
        for (auto &e : edges) {
            if (dist[e.u] != INT_MAX && dist[e.u] + e.w < dist[e.v]) {
                dist[e.v] = dist[e.u] + e.w;
            }
        }
    }

    // Step 2: Check for negative weight cycle
    for (auto &e : edges) {
        if (dist[e.u] != INT_MAX && dist[e.u] + e.w < dist[e.v]) {
            cout << "Graph contains a negative weight cycle!\n";
            return {};
        }
    }

    return dist;
}

int main() {
    int n = 5; // number of nodes
    vector<Edge> edges;

    // Example graph
    edges.push_back({0, 1, -1});
    edges.push_back({0, 2, 4});
    edges.push_back({1, 2, 3});
    edges.push_back({1, 3, 2});
    edges.push_back({1, 4, 2});
    edges.push_back({3, 2, 5});
    edges.push_back({3, 1, 1});
    edges.push_back({4, 3, -3});

    vector<int> dist = bellmanFord(n, edges, 0);

    if (!dist.empty()) {
        cout << "Shortest distances from source 0:\n";
        for (int i = 0; i < n; i++) {
            cout << "0 -> " << i << " = " << dist[i] << "\n";
        }
    }
}
```

---

## 🔹 Complexity

* **Time Complexity:** `O(V * E)`

  * `V-1` iterations over all `E` edges.
* **Space Complexity:** `O(V)`

  * Distance array.

---

## 🔹 When to Use Bellman–Ford

* Graphs with **negative edge weights**.
* Detecting **negative weight cycles**.
* Not efficient for large dense graphs compared to Dijkstra.

---

✅ Summary:

* **Dijkstra** → Faster, but **no negative weights**.
* **Bellman–Ford** → Handles **negative weights & detects negative cycles**, but slower.

---
