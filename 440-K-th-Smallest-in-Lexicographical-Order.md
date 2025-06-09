# 🔢 K-th Smallest in Lexicographical Order - LeetCode 440

## 📄 Problem Statement

Given two integers `n` and `k`, return the **k-th lexicographically smallest integer** in the range `[1, n]`.

**Constraints:**
- `1 <= k <= n <= 10^9`

🔗 [View on LeetCode](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order)

---

## 🧠 Intuition

This problem is related to **lexicographic (dictionary) order traversal**. If we write all numbers from `1` to `n` in lexicographical order, the task is to find the k-th number in that list.

💡 **Key idea:**  
Visualize the lexicographical order as a **prefix tree (Trie)** of digits. Perform a **controlled DFS-like traversal**, but count how many numbers are under each prefix to skip entire subtrees efficiently.

---

## 🛠️ Approach

1. Start at number `1` (the smallest prefix).
2. At each step, calculate how many numbers (`steps`) exist between the current prefix `curr` and the next prefix `curr + 1`.
3. If `steps <= k`, skip the whole subtree (`curr++`), decrease `k` by `steps`.
4. If `steps > k`, go **deeper** in the tree (`curr *= 10`), and decrease `k` by `1` (for moving into `curr`).
5. Repeat until `k == 0`.

### 🔧 countSteps(n, first, last)
This helper function calculates how many numbers exist between two prefixes `[first, last)` under the constraint `n`.

---

## 💻 Code

```cpp
class Solution {
public:
    int findKthNumber(int n, int k) {
        int curr = 1;
        k--; // First number is 1, so we need to find k-1 more

        while (k > 0) {
            long long steps = countSteps(n, curr, curr + 1);
            if (steps <= k) {
                curr++;        // Skip the current prefix
                k -= steps;
            } else {
                curr *= 10;    // Go deeper under the current prefix
                k--;
            }
        }
        return curr;
    }

private:
    long long countSteps(int n, long long first, long long last) {
        long long steps = 0;
        while (first <= n) {
            steps += min((long long)n + 1, last) - first;
            first *= 10;
            last *= 10;
        }
        return steps;
    }
};
```
## 🔍 Example

**Input:**  
`n = 100, k = 10` 

**Lexicographical Order**
`1, 10, 100, 11, 12, 13, ..., 2, 20, ...`

**Output:**  
`17`  

**Explanation:**  
- In dictionary order:
  `1,10,11,12,13,14,15,16,17`

---
## ⏱️ Time and Space Complexity

| Type               | Complexity       |
|--------------------|------------------|
| 🕒 Time Complexity  | O(log n)             |
| 🗂 Space Complexity | O(1) |

- We traverse a prefix tree, and at each step, count how many nodes (numbers) exist in a subtree.
- The tree has height ≈ `log₁₀(n)`, and we move across or down the tree efficiently using arithmetic (not recursion).

---

## ✅ Why This Works

- Lexicographical order can be modeled as a **10-ary tree**, where each node represents a number and its children are formed by appending digits (e.g., 1 → 10, 11, 12, ...).
- By counting how many nodes are in each subtree, we can decide whether to **dive deeper** or **skip the subtree**.
- This greedy prefix-based traversal avoids building the entire list — essential for `n` up to `10^9`.

---

## 📌 Key Takeaways

- ⚡ Prefix-counting strategy avoids TLE for large `n`.
- 🧠 Lexical order can be viewed as a traversal over a virtual Trie.
- 🔢 Problem teaches **digit-based traversal** and efficient **tree pruning** techniques.
- 🪜 Advanced greedy + combinatorics + number theory concept.

---

## 🏷️ Tags

`Greedy` • `Trie` • `Lexicographical Order` • `Tree Traversal` • `Prefix Tree` • `LeetCode Hard`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
