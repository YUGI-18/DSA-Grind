
# 📌 Disjoint Set Union (DSU / Union-Find)

---

## 🔹 What is Disjoint Set Union?

Disjoint Set Union (DSU) is a data structure that keeps track of a set of elements partitioned into **disjoint (non-overlapping) subsets**.
It supports two main operations efficiently:

1. **Find** → Determine which subset an element belongs to (with **path compression**).
2. **Union** → Merge two subsets into one (optimized by **rank** or **size**).

It is commonly used in:

* **Kruskal’s Algorithm** (for MST).
* Detecting **cycles** in graphs.
* **Connected components** problems.

---

## 🔹 Process (Step by Step)

1. **Initialization**

   * Each node is its own parent initially.

2. **Find with Path Compression**

   * When finding the root of a node, recursively update its parent to the root for efficiency.

3. **Union by Rank / Size**

   * **By Rank:** Attach the shorter tree under the taller tree.
   * **By Size:** Attach the smaller set under the larger set.

---

## 🔹 Template Code (Class)

```cpp
#include <bits/stdc++.h>
using namespace std;

class DSU {
    vector<int> parent, rank, size;

public:
    DSU(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        size.resize(n, 1);
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    // Find with path compression
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    // Union by rank
    bool unionByRank(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (pu == pv) return false;

        if (rank[pu] < rank[pv]) {
            parent[pu] = pv;
        } else if (rank[pu] > rank[pv]) {
            parent[pv] = pu;
        } else {
            parent[pv] = pu;
            rank[pu]++;
        }
        return true;
    }

    // Union by size
    bool unionBySize(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (pu == pv) return false;

        if (size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pu];
        } else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
        return true;
    }
};
```

---

## 🔹 Complexity

* **Find (with path compression):** `O(α(N))` ≈ constant time.
* **Union (with rank/size):** `O(α(N))` ≈ constant time.
* **Space Complexity:** `O(N)`

Here, `α(N)` = **inverse Ackermann function**, which grows extremely slowly (practically ≤ 4 for all real inputs).

---

## 🔹 When to Use DSU?

✅ Use DSU when:

* You need to check if two nodes belong to the **same connected component**.
* You need efficient **merge and query operations** on sets.
* Algorithms like **Kruskal’s MST**, **cycle detection**, **dynamic connectivity**.

---
