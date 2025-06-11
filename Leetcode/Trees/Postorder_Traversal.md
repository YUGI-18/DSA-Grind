# 🌳 Binary Tree Postorder Traversal

## 📝 Problem Statement

Given the root of a binary tree, return the postorder traversal of its nodes' values.

---

## ✨ Examples

### Example 1:

**Input:**

```cpp
root = [1,null,2,3]
```

**Output:**

```cpp
[3,2,1]
```

---

### Example 2:

**Input:**

```cpp
root = [1,2,3,4,5,null,8,null,null,6,7,9]
```

**Output:**

```cpp
[4,6,7,5,2,9,8,3,1]
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

## 🚀 Approach

1. Use a stack to simulate recursion.
2. Traverse the left subtree first by pushing nodes.
3. Check the right child of the node.
4. If the right child is null or already visited, process the current node.
5. Repeat the process until all nodes are visited.

---

## 🔢 Code Implementation

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> postorder;
        if (root == NULL) return postorder;
        stack<TreeNode*> st;
        TreeNode* cur = root;
        TreeNode* temp;
        while (cur != NULL || !st.empty()) {
            if (cur != NULL) {
                st.push(cur);
                cur = cur->left;
            } else {
                temp = st.top()->right;
                if (temp == NULL) {
                    temp = st.top();
                    st.pop();
                    postorder.push_back(temp->val);
                    while (!st.empty() && temp == st.top()->right) {
                        temp = st.top();
                        st.pop();
                        postorder.push_back(temp->val);
                    }
                } else {
                    cur = temp;
                }
            }
        }
        return postorder;
    }
};
```

---

## ⏱ Time Complexity

* **O(n)** — each node is visited once.

## 📂 Space Complexity

* **O(n)** — in the worst case, all nodes are pushed into the stack.

---

## 🔧 Constraints

* The number of nodes in the tree is in the range `[0, 100]`
* `-100 <= Node.val <= 100`

---

## 🌟 Key Points

* Postorder traversal: Left -> Right -> Root
* Stack is used to mimic recursive traversal iteratively
