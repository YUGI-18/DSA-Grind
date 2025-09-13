
# 📌 Dijkstra’s Algorithm Templates (C++)

---

## 🔹 What is Dijkstra’s Algorithm?

Dijkstra’s Algorithm finds the **shortest path from a source node to all other nodes** in a graph with **non-negative edge weights**.
It is a **greedy algorithm** that expands the closest unvisited node first.

---

## 🔹 1. Dijkstra using **Priority Queue (Min-Heap)**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> dijkstraPQ(int n, vector<vector<pair<int, int>>>& adj, int src) {
    vector<int> dist(n, INT_MAX);
    dist[src] = 0;

    // Min-heap: {distance, node}
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
    pq.push({0, src});

    while (!pq.empty()) {
        int d = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        if (d > dist[u]) continue; // Skip if outdated

        for (auto [v, w] : adj[u]) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}
```

### ✅ Complexity

* **Time:** `O((V + E) log V)`
* **Space:** `O(V)`

### ✅ When to Use

* Works well when **graph is dense or large**.
* Most common and efficient implementation in practice.
* May store **duplicate nodes** in the PQ (lazy deletion), but still correct.

---

## 🔹 2. Dijkstra using **Set (Balanced BST)**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> dijkstraSet(int n, vector<vector<pair<int, int>>>& adj, int src) {
    vector<int> dist(n, INT_MAX);
    dist[src] = 0;

    // Set: {distance, node}
    set<pair<int, int>> st;
    st.insert({0, src});

    while (!st.empty()) {
        auto it = *st.begin();
        st.erase(st.begin());

        int d = it.first;
        int u = it.second;

        for (auto [v, w] : adj[u]) {
            if (dist[u] + w < dist[v]) {
                if (dist[v] != INT_MAX) {
                    st.erase({dist[v], v});
                }
                dist[v] = dist[u] + w;
                st.insert({dist[v], v});
            }
        }
    }
    return dist;
}
```

### ✅ Complexity

* **Time:** `O((V + E) log V)`
* **Space:** `O(V)`

### ✅ When to Use

* Ensures **no duplicates** in the data structure.
* Best when you need a **guaranteed clean structure** at all times.
* Slightly **slower than PQ** in practice due to balanced BST overhead.

---

## 🔹 Summary Table

| Version            | Data Structure | Time Complexity    | Space Complexity | Best Use Case                            |
| ------------------ | -------------- | ------------------ | ---------------- | ---------------------------------------- |
| **Dijkstra (PQ)**  | Min-heap       | `O((V + E) log V)` | `O(V)`           | Large/dense graphs, faster in practice   |
| **Dijkstra (Set)** | Balanced BST   | `O((V + E) log V)` | `O(V)`           | When you want no duplicates in structure |

---

## 🔹 Key Notes

* Dijkstra does **NOT** work with **negative weight edges**.
* Use **BFS** instead if edges are **unweighted**.
* For graphs with **negative weights**, use **Bellman-Ford**.
* For **all-pairs shortest path**, use **Floyd-Warshall** or run Dijkstra from each node.

---
