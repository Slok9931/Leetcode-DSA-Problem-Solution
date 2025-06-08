# 🌳 Kth Smallest Element in a BST - LeetCode 230

## 📄 Problem Statement

Given the `root` of a **Binary Search Tree (BST)** and an integer `k`, return the **kᵗʰ smallest element** in the BST.

BST has the property that **in-order traversal** gives values in **sorted order**.  
So the `kᵗʰ` node visited in an in-order traversal is the answer.

🔗 [View on LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

---

## 🧠 Intuition

Since an **in-order traversal** of a BST visits nodes in ascending order, we can:

- Traverse the tree **in-order** (Left → Node → Right)
- Keep a **counter** as we visit each node
- When the counter reaches `k`, we've found the answer

This avoids having to store all node values in an array.

---

## 🛠️ Approach

1. Perform an **in-order traversal** (DFS).
2. Maintain a **counter** to track how many nodes we've visited.
3. When `count == k`, store the `node->val` as the result.
4. Use pass-by-reference for `count` and `ans` to maintain state during recursion.

---

## 💻 Code

```cpp
class Solution {
public:
    void inOrderTraversal(TreeNode* root, int & count, int & ans, int k){
        if (root == NULL) return;
        
        inOrderTraversal(root->left, count, ans, k);
        
        count++;
        if (count == k) {
            ans = root->val;
            return;
        }

        inOrderTraversal(root->right, count, ans, k);
    }

    int kthSmallest(TreeNode* root, int k) {
        int count = 0, ans = -1;
        inOrderTraversal(root, count, ans, k);
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
```
      3
     / \
    1   4
     \
      2

k = 1
``` 

**Output:**  
`1`  

**Explanation:**  
- n-order traversal: `[1, 2, 3, 4]` → 1st smallest = `1`

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(H + k), H = tree height |
| 🗂 Space Complexity | O(H) recursion stack |

- In the worst case, we may visit up to `k` nodes.
- The height `H` of the tree contributes to recursive stack usage.

---

## ✅ Why This Works

- In-order traversal yields sorted values in a BST.
- We traverse nodes one-by-one until the `kᵗʰ` smallest is found.
- Using references avoids extra memory for arrays/lists.

---

## 📌 Key Takeaways

- 📚 **In-order traversal** of BST = sorted order of elements
- 🔢 Track position with a counter to find `kᵗʰ` smallest efficiently
- 🧠 Pass-by-reference helps avoid global variables or unnecessary returns
- 🌿 A minimal recursive DFS solves the problem with **O(1) extra space** beyond the recursion stack

---

## 🏷️ Tags

`Binary Search Tree` • `Inorder Traversal` • `DFS` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
