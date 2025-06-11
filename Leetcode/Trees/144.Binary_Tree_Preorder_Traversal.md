# 🌲 Binary Tree Preorder Traversal

## 📝 Problem Statement

Given the root of a binary tree, return the **preorder traversal** of its nodes' values.

---

## ✨ Examples

### Example 1:

**Input:**

```cpp
root = [1,null,2,3]
```

**Output:**

```cpp
[1,2,3]
```

### Example 2:

**Input:**

```cpp
root = [1,2,3,4,5,null,8,null,null,6,7,9]
```

**Output:**

```cpp
[1,2,4,5,6,7,3,8,9]
```

### Example 3:

**Input:**

```cpp
root = []
```

**Output:**

```cpp
[]
```

### Example 4:

**Input:**

```cpp
root = [1]
```

**Output:**

```cpp
[1]
```

---

## 🚀 Approach: Iterative Preorder Traversal Using Stack

### *Algorithm*

1. Initialize an empty vector `preorder`.
2. If the root is `NULL`, return the empty vector.
3. Use a stack to simulate the recursive preorder traversal:

   * Push the root node onto the stack.
   * While the stack is not empty:

     * Pop the top node and add its value to the `preorder` vector.
     * Push the right child (if exists), then the left child (if exists).
4. Return the `preorder` vector.

---

## 🔢 Code Implementation

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> preorder;
        if(root == NULL) return preorder;

        stack<TreeNode*> st;
        st.push(root);
        while(!st.empty()) {
            root = st.top();
            st.pop();
            preorder.push_back(root->val);
            if(root->right != NULL) {
                st.push(root->right);
            }
            if(root->left != NULL) {
                st.push(root->left);
            }
        }
        return preorder;
    }
};
```

---

## ⏱ Time Complexity

* **O(n)** — where `n` is the number of nodes in the tree (each node is visited once).

## 💾 Space Complexity

* **O(n)** — for the stack in the worst case (completely unbalanced tree).

---

## 🔧 Constraints

* The number of nodes in the tree is in the range `[0, 100]`
* `-100 <= Node.val <= 100`

---

## 🌟 Key Points

* Preorder traversal: **Root → Left → Right**
* Stack-based iterative method avoids recursion and keeps constant control over memory usage.
