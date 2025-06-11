# 🌳 Binary Tree Level Order Traversal

## 📝 Problem Statement

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

---

## ✨ Examples

### Example 1:

**Input:**

```cpp
root = [3,9,20,null,null,15,7]
```

**Output:**

```cpp
[[3],[9,20],[15,7]]
```

---

### Example 2:

**Input:**

```cpp
root = [1]
```

**Output:**

```cpp
[[1]]
```

---

### Example 3:

**Input:**

```cpp
root = []
```

**Output:**

```cpp
[]
```

---

## 🚀 Approach

1. Use a queue to traverse the tree level by level.
2. At each level, process all nodes currently in the queue.
3. For each node, add its value to the current level list.
4. Push its left and right children into the queue if they exist.
5. Append the level list to the final result.

---

## 🔢 Code Implementation

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> levelorder;
        if (root == NULL) return levelorder;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            int size = q.size();
            vector<int> level;
            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();
                if (node->left != NULL) q.push(node->left);
                if (node->right != NULL) q.push(node->right);
                level.push_back(node->val);
            }
            levelorder.push_back(level);
        }
        return levelorder;
    }
};
```

---

## ⏱ Time Complexity

* **O(n)** — each node is visited once.

## 💾 Space Complexity

* **O(n)** — to store nodes in the queue and result.

---

## 🔧 Constraints

* The number of nodes in the tree is in the range `[0, 2000]`
* `-1000 <= Node.val <= 1000`

---

## 🌟 Key Points

* Level Order Traversal: Traverses tree level-by-level.
* Queue is used to handle nodes in FIFO order for level-wise processing.
