
# 📌 Tarjan’s Algorithm (for Strongly Connected Components – SCC)

---

## 🔹 What is Tarjan’s Algorithm?

Tarjan’s Algorithm is another efficient method to find **Strongly Connected Components (SCCs)** in a directed graph.
Unlike **Kosaraju’s**, it does it in **one DFS traversal** using **low-link values**.

---

## 🔹 Process (Step by Step)

1. Maintain:

   * `disc[node]` → discovery time of node.
   * `low[node]` → lowest discovery time reachable from that node.
   * `stack` → nodes in the current DFS path.
   * `inStack[]` → marks whether a node is in the stack.

2. DFS Traversal:

   * Assign discovery time & low value.
   * Explore neighbors:

     * If not visited → DFS on neighbor, update `low[node] = min(low[node], low[nei])`.
     * If in stack → update `low[node] = min(low[node], disc[nei])`.

3. If `low[node] == disc[node]`, then `node` is the root of a SCC.

   * Pop nodes from stack until `node` is reached.

---

## 🔹 Template Code (Without `main`)

```cpp
#include <bits/stdc++.h>
using namespace std;

class TarjanSCC {
    int n, timer;
    vector<vector<int>> adj;
    vector<int> disc, low, inStack;
    stack<int> st;
    vector<vector<int>> sccs;

public:
    TarjanSCC(int n) {
        this->n = n;
        adj.resize(n);
        disc.assign(n, -1);
        low.assign(n, -1);
        inStack.assign(n, 0);
        timer = 0;
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    void dfs(int u) {
        disc[u] = low[u] = timer++;
        st.push(u);
        inStack[u] = 1;

        for (int v : adj[u]) {
            if (disc[v] == -1) {
                dfs(v);
                low[u] = min(low[u], low[v]);
            } else if (inStack[v]) {
                low[u] = min(low[u], disc[v]);
            }
        }

        // If u is head of SCC
        if (low[u] == disc[u]) {
            vector<int> component;
            while (true) {
                int node = st.top(); st.pop();
                inStack[node] = 0;
                component.push_back(node);
                if (node == u) break;
            }
            sccs.push_back(component);
        }
    }

    vector<vector<int>> getSCCs() {
        for (int i = 0; i < n; i++) {
            if (disc[i] == -1) dfs(i);
        }
        return sccs;
    }
};
```

---

## 🔹 Complexity

* **Time Complexity:** `O(V + E)`
* **Space Complexity:** `O(V + E)`

---

## 🔹 When to Use Tarjan?

✅ Use when:

* You need to find SCCs **in a single DFS traversal**.
* More efficient for large graphs compared to Kosaraju.
* Common in:

  * **Compiler optimizations** (dependency graphs).
  * **Deadlock detection**.
  * **2-SAT problems**.

---
