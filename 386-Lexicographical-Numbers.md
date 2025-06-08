# 🔢 Lexicographical Numbers - LeetCode 386

## 📄 Problem Statement

Given an integer `n`, return all the numbers in the range `[1, n]` sorted in **lexicographical order**.

You **must write an algorithm that runs in `O(n)` time** and uses **`O(1)` extra space** (excluding the output array).

🔗 [View on LeetCode](https://leetcode.com/problems/lexicographical-numbers)

---

## 🧠 Intuition

We are asked to generate numbers from 1 to `n` in **dictionary order**, not numeric order.

For example:
```
Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]
```

This structure resembles a **tree traversal**:
- 1 → 10 → 100, 101,...  
- 2 → 20 → 200,... and so on.

This naturally leads us to a **Depth-First Search (DFS)** approach.

---

## 🛠️ Approach

1. Start DFS from numbers `1` to `9`.
2. For each number, go deeper by multiplying it by 10 and adding digits `0-9`.
3. Stop recursion if the new number exceeds `n`.

This method guarantees `O(n)` traversal time, and since we don't use extra structures apart from the result vector, it satisfies the space constraint too.

---

## 💻 Code

```cpp
class Solution {
public:
    void dfs(int curr, int n, vector<int>& ans) {
        if (curr > n) return;
        ans.push_back(curr);
        for (int i = 0; i < 10; i++) {
            int next = curr * 10 + i;
            if (next > n) return;
            dfs(next, n, ans);
        }
    }

    vector<int> lexicalOrder(int n) {
        vector<int> ans;
        for (int i = 1; i <= 9; i++) {
            dfs(i, n, ans);
        }
        return ans;
    }
};
```
## 🔍 Example

**Input:**  
`n = 13` 

**Output:**  
`[1,10,11,12,13,2,3,4,5,6,7,8,9]`  

**Explanation:**  
- In dictionary order:
  `1 → 10,11,12,13 → 2 → 3 → ... → 9`

---
## ⏱️ Time and Space Complexity

| Type               | Complexity       |
|--------------------|------------------|
| 🕒 Time Complexity  | O(n)             |
| 🗂 Space Complexity | O(1) extra space (excluding output) |

- The DFS visits each number **exactly once**, hence `O(n)` time.
- No additional data structures (like sorting arrays or hash maps) are used.
- The only space used is the output vector `ans`, which is required.

---

## ✅ Why This Works

- **Lexicographical order** mimics a **prefix-tree (trie)** structure, where children of node `x` are `x0` to `x9`.
- Starting DFS from 1 to 9 and diving deeper using `curr * 10 + i` explores the tree in lexicographic order.
- **Pruning** when `curr > n` avoids unnecessary recursion, ensuring we stay within bounds.
- Since each number is processed once and no sorting is done, it meets the `O(n)` time and `O(1)` extra space constraints.

---

## 📌 Key Takeaways

- 📚 Lexical order can be **modeled as a DFS traversal** of an implicit tree.
- 🔍 Instead of sorting numbers, we **generate** them in the required order.
- ⏳ DFS ensures **efficient traversal**, pruning avoids invalid paths.
- 💡 Useful pattern when **generating ordered sequences without sorting**.
- ✅ Carefully designed recursion can be more optimal than brute-force or sort-based solutions.

---

## 🏷️ Tags

`DFS` • `Graph` • `Lexicographical Order` • `Tree Traversal` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
