
# BFS and DFS Templates in C++

This repository contains clean **C++ templates** for BFS and DFS along with **explanations** and **use cases**.

---

## 📌 BFS (Breadth First Search)

### 🔹 Code Template

```cpp
#include <bits/stdc++.h>
using namespace std;

void bfs(int start, vector<vector<int>>& adj, int n) {
    vector<bool> visited(n, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " "; // process node

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int n = 6; // number of nodes
    vector<vector<int>> adj(n);

    // Example edges (undirected graph)
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0, 4};
    adj[3] = {1, 5};
    adj[4] = {1, 2, 5};
    adj[5] = {3, 4};

    cout << "BFS starting from node 0: ";
    bfs(0, adj, n);
}
```

### 🔹 Explanation

* BFS explores the graph **level by level** (like ripples in water).
* Uses a **queue** to maintain the current frontier.
* Guarantees the **shortest path** in unweighted graphs.

### 🔹 When to Use BFS

* Find **shortest path** in unweighted graphs.
* Solve **minimum steps problems** (e.g., word ladder, knight moves, shortest path in grid).
* Explore nodes in **layers**.

---

### ✅ Complexity

* **Time Complexity:** `O(V + E)`

  * Each vertex is enqueued/dequeued once → `O(V)`
  * Each edge is checked once → `O(E)`
* **Space Complexity:** `O(V)`

  * `visited[]` array + `queue` (at worst all vertices in a level)

### ✅ Notes

* Best for **shortest path in unweighted graphs**.
* Works in **layers** (level-order traversal).

---

## 📌 DFS (Depth First Search) – Recursive

### 🔹 Code Template

```cpp
#include <bits/stdc++.h>
using namespace std;

void dfs_recursive(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " "; // process node

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs_recursive(neighbor, adj, visited);
        }
    }
}

int main() {
    int n = 6;
    vector<vector<int>> adj(n);

    // Example edges
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0, 4};
    adj[3] = {1, 5};
    adj[4] = {1, 2, 5};
    adj[5] = {3, 4};

    vector<bool> visited(n, false);
    cout << "DFS starting from node 0: ";
    dfs_recursive(0, adj, visited);
}
```

### 🔹 Explanation

* DFS goes **deep into one path** before backtracking.
* Uses **recursion (system stack)** to explore nodes.
* Can be used to detect **cycles** and explore **connected components**.

### 🔹 When to Use Recursive DFS

* When graph/tree depth is not too large (avoid stack overflow).
* Problems involving **backtracking** (e.g., N-Queens, path finding, word search).
* Useful for **connected components** and **cycle detection**.

---

### ✅ Complexity

* **Time Complexity:** `O(V + E)`

  * Each vertex visited once → `O(V)`
  * Each edge explored once → `O(E)`
* **Space Complexity:** `O(V)`

  * `visited[]` array + recursion call stack (worst case depth = `V`)

### ✅ Notes

* Good for **cycle detection**, **connected components**, **backtracking problems**.
* Risk of **stack overflow** in deep graphs.

---

## 📌 DFS (Depth First Search) – Iterative with Stack

### 🔹 Code Template

```cpp
#include <bits/stdc++.h>
using namespace std;

void dfs_iterative(int start, vector<vector<int>>& adj, int n) {
    vector<bool> visited(n, false);
    stack<int> st;
    st.push(start);

    while (!st.empty()) {
        int node = st.top();
        st.pop();

        if (!visited[node]) {
            visited[node] = true;
            cout << node << " "; // process node

            // Push neighbors in reverse order to mimic recursion
            for (auto it = adj[node].rbegin(); it != adj[node].rend(); it++) {
                if (!visited[*it]) {
                    st.push(*it);
                }
            }
        }
    }
}

int main() {
    int n = 6;
    vector<vector<int>> adj(n);

    // Example edges
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0, 4};
    adj[3] = {1, 5};
    adj[4] = {1, 2, 5};
    adj[5] = {3, 4};

    cout << "DFS (iterative) starting from node 0: ";
    dfs_iterative(0, adj, n);
}
```

### 🔹 Explanation

* Same as recursive DFS, but uses an **explicit stack**.
* Avoids **stack overflow** on large/deep graphs.
* Gives more **control** over traversal order.

### 🔹 When to Use Iterative DFS

* When recursion depth might exceed system limits (e.g., graphs with 10⁵+ nodes).
* When you want more control over **order of visiting nodes**.
* When implementing DFS in environments that discourage recursion.

---

### ✅ Complexity

* **Time Complexity:** `O(V + E)`

  * Same reasoning as recursive DFS
* **Space Complexity:** `O(V)`

  * `visited[]` array + explicit stack

### ✅ Notes

* Same as recursive DFS but avoids recursion depth issues.
* More control over node visiting order.

---


## 🔹 Summary Table

| Algorithm           | Time Complexity | Space Complexity | Best Use Case                                       |
| ------------------- | --------------- | ---------------- | --------------------------------------------------- |
| **BFS**             | `O(V + E)`      | `O(V)`           | Shortest path in unweighted graphs, minimum steps   |
| **DFS (Recursive)** | `O(V + E)`      | `O(V)`           | Cycle detection, connected components, backtracking |
| **DFS (Iterative)** | `O(V + E)`      | `O(V)`           | Large graphs, avoids recursion depth issues         |

---

🚀 **Tip for Interviews:**

* Use **BFS** when asked about **shortest path / minimum steps**.
* Use **DFS** for **exploration, cycle detection, connectivity, backtracking**.

---

