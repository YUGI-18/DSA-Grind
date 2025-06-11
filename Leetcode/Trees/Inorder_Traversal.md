# 🌳 Binary Tree Inorder Traversal

## 📝 Problem Statement

Given the root of a binary tree, return the inorder traversal of its nodes' values.

---

## ✨ Examples

### Example 1:

**Input:**

```cpp
root = [1,null,2,3]
```

**Output:**

```cpp
[1,3,2]
```

---

### Example 2:

**Input:**

```cpp
root = [1,2,3,4,5,null,8,null,null,6,7,9]
```

**Output:**

```cpp
[4,2,6,5,7,1,3,9,8]
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

1. Use a stack to simulate the recursion for inorder traversal.
2. Traverse left subtree until the end and push nodes into the stack.
3. Visit node, then traverse the right subtree.
4. Repeat until the stack is empty and all nodes are visited.

---

## 🔢 Code Implementation

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> inorder;
        if(root == NULL) return inorder;
        stack<TreeNode*> st;
        TreeNode* node = root;
        while(true){
            if(node != NULL){
                st.push(node);
                node = node->left;
            }
            else {
                if(st.empty()) break;
                node = st.top();
                st.pop();
                inorder.push_back(node->val);
                node = node->right;
            }
        }
        return inorder;
    }
};
```

---

## ⏱ Time Complexity

* **O(n)** — each node is visited once.

## 💾 Space Complexity

* **O(n)** — in the worst case (unbalanced tree), all nodes might be pushed to the stack.

---

## 🔧 Constraints

* The number of nodes in the tree is in the range `[0, 100]`
* `-100 <= Node.val <= 100`

---

## 🌟 Key Points

* Inorder traversal: Left -> Root -> Right
* Stack is used to mimic recursive call stack for iterative solution
