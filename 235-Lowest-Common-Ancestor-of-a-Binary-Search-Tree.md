# 🌳 Lowest Common Ancestor of a Binary Search Tree - LeetCode 235

## 📄 Problem Statement

Given a **Binary Search Tree (BST)**, find the **lowest common ancestor (LCA)** of two given nodes `p` and `q`.

According to the **definition of LCA**:
> The lowest common ancestor is the lowest node in the tree that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).

🔗 [View on LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

---

## 🧠 Intuition

This problem is a classic **Lowest Common Ancestor** problem.  
Although it's in a BST, your current approach solves it using the **general Binary Tree LCA** technique.

In a binary tree:
- If one node is found in the left subtree and the other in the right subtree → current node is LCA.
- If both are in the same subtree → propagate that subtree’s return value upward.

---

## 🛠️ Approach

1. Traverse the tree from the root.
2. If the current node is `NULL`, return `NULL`.
3. If the current node matches either `p` or `q`, return it.
4. Recursively search in the left and right subtrees.
5. If both sides return non-null nodes, the current node is the **LCA**.
6. If only one side returns a node, propagate it upward.

---

## 💻 Code

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL) return NULL;
        if (root->val == p->val || root->val == q->val) return root;

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if (left && right) return root;
        return left ? left : right;
    }
};
```
---

## 🔍 Example

**Input:**  
```
        6
       / \
      2   8
     / \ / \
    0  4 7  9
      / \
     3   5

p = 2, q = 8
``` 

**Output:**  
`6`  

**Explanation:**  
- Nodes 2 and 8 are in different subtrees of 6, so 6 is their LCA.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(h) |

- `n` is the number of nodes in the tree.
- `h` is the height of the tree, which affects the recursion stack.

---

## ✅ Why This Works

- This solution performs a **post-order traversal**, checking both left and right subtrees before deciding.
- If both left and right return a non-null node, the current node must be their common ancestor.
- If only one side returns non-null, that means both `p` and `q` lie in the same subtree.

---

## 📌 Key Takeaways

- 🌳 This is the general approach for **Binary Tree** LCA, not just BSTs.
- 🧠 No need to use BST properties in this solution.
- 🔄 Recursive solutions are intuitive for LCA problems.
- 📦 Can be easily extended to handle cases where either node might not be present.

---

## 🧠 Optimised BST-Based Intuition

Since the tree is a **Binary Search Tree (BST)**, we can use its properties to **optimize** the search:

- If both `p` and `q` are **greater** than the current node → move to the **right subtree**.
- If both are **less** → move to the **left subtree**.
- Otherwise, the current node is the **split point**, hence the **lowest common ancestor**.

---

## 🛠️ Optimized BST-Based Approach

1. Start from the root node.
2. If both `p` and `q` are greater than the root, move to `root->right`.
3. If both are less, move to `root->left`.
4. If one is on the left and the other is on the right (or one equals the root), the current root is the LCA.

---

## 💻 Code

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while (root) {
            if (p->val > root->val && q->val > root->val) {
                root = root->right;  // Both nodes lie in the right subtree
            } else if (p->val < root->val && q->val < root->val) {
                root = root->left;   // Both nodes lie in the left subtree
            } else {
                return root;  // Split point found; this is the LCA
            }
        }
        return nullptr;   
    }
};
```

## 🏷️ Tags

`Binary Tree` • `Binary Search Tree` • `DFS` • `Recursion` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
