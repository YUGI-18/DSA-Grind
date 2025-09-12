
# 📌 Topological Sort 

Topological sort orders nodes in a **Directed Acyclic Graph (DAG)** such that for every edge `u → v`, node `u` appears before `v`.

---

## 🔹 1. Topological Sort using **DFS**

### ✅ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void dfs(int node, vector<vector<int>>& adj, vector<bool>& visited, stack<int>& st) {
    visited[node] = true;

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adj, visited, st);
        }
    }

    st.push(node); // push after visiting neighbors
}

vector<int> topoSortDFS(int n, vector<vector<int>>& adj) {
    vector<bool> visited(n, false);
    stack<int> st;

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i, adj, visited, st);
        }
    }

    vector<int> topo;
    while (!st.empty()) {
        topo.push_back(st.top());
        st.pop();
    }
    return topo;
}

int main() {
    int n = 6; // number of nodes
    vector<vector<int>> adj(n);

    // Directed edges
    adj[5] = {0, 2};
    adj[4] = {0, 1};
    adj[2] = {3};
    adj[3] = {1};

    vector<int> topo = topoSortDFS(n, adj);

    cout << "Topological Order (DFS): ";
    for (int node : topo) cout << node << " ";
}
```

### ✅ Complexity

* **Time Complexity:** `O(V + E)`

  * Each node visited once → `O(V)`
  * Each edge explored once → `O(E)`
* **Space Complexity:** `O(V)`

  * Visited array + recursion stack + output vector

### ✅ When to Use

* If recursion is okay (graph depth is not too big).
* Problems like **course schedule**, **dependency resolution**.

---

## 🔹 2. Topological Sort using **Kahn’s Algorithm (BFS + Indegree)**

### ✅ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> topoSortKahn(int n, vector<vector<int>>& adj) {
    vector<int> indegree(n, 0);

    // Calculate indegree
    for (int u = 0; u < n; u++) {
        for (int v : adj[u]) {
            indegree[v]++;
        }
    }

    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) q.push(i);
    }

    vector<int> topo;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        topo.push_back(node);

        for (int neighbor : adj[node]) {
            indegree[neighbor]--;
            if (indegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    return topo;
}

int main() {
    int n = 6; // number of nodes
    vector<vector<int>> adj(n);

    // Directed edges
    adj[5] = {0, 2};
    adj[4] = {0, 1};
    adj[2] = {3};
    adj[3] = {1};

    vector<int> topo = topoSortKahn(n, adj);

    cout << "Topological Order (Kahn's): ";
    for (int node : topo) cout << node << " ";
}
```

### ✅ Complexity

* **Time Complexity:** `O(V + E)`

  * Each node enqueued/dequeued once → `O(V)`
  * Each edge processed once → `O(E)`
* **Space Complexity:** `O(V)`

  * Indegree array + queue + output vector

### ✅ When to Use

* When recursion depth may cause stack overflow.
* When you also need to **detect cycles** (if topo order has fewer than `V` nodes, the graph has a cycle).

---

## 🔹 Summary: DFS vs Kahn’s Algorithm

| Method               | Time Complexity | Space Complexity | Pros                       | Cons                               |
| -------------------- | --------------- | ---------------- | -------------------------- | ---------------------------------- |
| **DFS-based**        | `O(V + E)`      | `O(V)`           | Simple, natural recursion  | Stack overflow on very deep graphs |
| **Kahn’s Algorithm** | `O(V + E)`      | `O(V)`           | Iterative, cycle detection | Needs indegree calculation         |

---

🚀 **Tip:**

* Use **DFS Topo Sort** when recursion is safe and graph size is moderate.
* Use **Kahn’s Algorithm** for **large graphs** or when cycle detection is required.

---
