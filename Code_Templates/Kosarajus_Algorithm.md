
# 📌 Kosaraju’s Algorithm (for Strongly Connected Components – SCC)

---

## 🔹 What is Kosaraju’s Algorithm?

Kosaraju’s Algorithm is used to find **Strongly Connected Components (SCCs)** in a **directed graph**.
A **SCC** is a maximal group of vertices such that each vertex is reachable from every other vertex in the group.

---

## 🔹 Process (Step by Step)

1. **Do a DFS traversal** on the graph and push nodes onto a stack in the order of their **finishing time**.

   * Finishing time = when DFS returns from a node.

2. **Reverse the graph** (transpose: reverse all edges).

3. **Do DFS again** in the order of nodes popped from the stack.

   * Each DFS call will give one **Strongly Connected Component**.

---

## 🔹 Template Code (Without `main`)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Kosaraju {
    int n;
    vector<vector<int>> adj, revAdj;
    vector<int> visited;
    stack<int> st;

public:
    Kosaraju(int n) {
        this->n = n;
        adj.resize(n);
        revAdj.resize(n);
        visited.assign(n, 0);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        revAdj[v].push_back(u); // reverse graph
    }

    // Step 1: DFS to fill stack by finish time
    void dfs1(int node) {
        visited[node] = 1;
        for (int nei : adj[node]) {
            if (!visited[nei]) dfs1(nei);
        }
        st.push(node);
    }

    // Step 2: DFS on reversed graph
    void dfs2(int node, vector<int>& component) {
        visited[node] = 1;
        component.push_back(node);
        for (int nei : revAdj[node]) {
            if (!visited[nei]) dfs2(nei, component);
        }
    }

    // Main function to get SCCs
    vector<vector<int>> getSCCs() {
        // Step 1: Fill order stack
        fill(visited.begin(), visited.end(), 0);
        for (int i = 0; i < n; i++) {
            if (!visited[i]) dfs1(i);
        }

        // Step 2: Process nodes in stack order on reversed graph
        fill(visited.begin(), visited.end(), 0);
        vector<vector<int>> sccs;

        while (!st.empty()) {
            int node = st.top(); st.pop();
            if (!visited[node]) {
                vector<int> component;
                dfs2(node, component);
                sccs.push_back(component);
            }
        }
        return sccs;
    }
};
```

---

## 🔹 Complexity

* **Time Complexity:** `O(V + E)`

  * Two DFS traversals + graph reversal.
* **Space Complexity:** `O(V + E)`

  * For adjacency lists, stack, recursion.

---

## 🔹 When to Use Kosaraju?

✅ Use when:

* You need to find **all strongly connected components** in a directed graph.
* Applications include:

  * **Deadlock detection** in operating systems.
  * **Optimizing compilers** (variable dependencies).
  * **Network analysis** (mutually reachable nodes).

---

