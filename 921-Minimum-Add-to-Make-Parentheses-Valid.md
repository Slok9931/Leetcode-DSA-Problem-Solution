# 🧮 Minimum Add to Make Parentheses Valid - LeetCode 921

## 📄 Problem Statement

A parentheses string is **valid** if:

- It is an empty string `""`, or
- It can be written as `AB` (A concatenated with B), where A and B are valid strings, or
- It can be written as `(A)`, where A is a valid string.

You are given a parentheses string `s`.  
In **one move**, you can **insert** either `'('` or `')'` at **any** position in the string.

🔁 Your goal is to **make the string valid** with the **minimum number of insertions**.

Return the **minimum number of moves** required to make `s` valid.

🔗 [View on LeetCode](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid)

---

## 🧠 Intuition

We are asked to **balance** the parentheses.

We can keep track of:
- The number of unmatched `'('` (open brackets that need a closing `')'`)
- The number of unmatched `')'` (closing brackets that appear without a matching `'('`)

We:
- Increment the `open` counter for every `'('`.
- Decrease `open` for every `')'` if there is an unmatched `'('`.
- Otherwise, we increment the answer since we need to insert a matching `'('`.

---

## 🛠️ Approach

1. Initialize two counters:
   - `open`: number of unmatched opening brackets `'('`.
   - `ans`: number of insertions needed for unmatched closing brackets `')'`.
2. Traverse the string character by character:
   - If it's `'('`, increment `open`.
   - If it's `')'`:
     - If `open > 0`, a match is found — decrement `open`.
     - Otherwise, increment `ans` (we need an extra `'('`).
3. Return the total number of insertions required: `ans + open`.

---

## 💻 Code

```cpp
class Solution {
public:
    int minAddToMakeValid(string s) {
        int open = 0, ans = 0;
        for(char c : s){
            if(c == '(') open++;
            else {
                if(open != 0) open--;
                else ans++;
            }
        }
        return ans + open;
    }
};
```

---

## 🔍 Example

**Input:**  
`s = "()))("` 

**Output:**  
`3`  

**Explanation:**  
- We need 1 `'('` before the first `')'` and 2 `')'` after the unmatched `'('`.

Final valid string: `(()))()`

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) — Traverse string once |
| 🗂 Space Complexity | O(1) |

- Every element is processed at most twice due to the sliding window.

---

## ✅ Why This Works

By counting unmatched opening and closing brackets:
  - We handle each character in **constant time**.
  - We don’t need to use stacks — only simple counters.
This greedy approach ensures the minimum number of insertions.

---

## 📌 Key Takeaways

- Matching parentheses problems can often be solved using **simple counters** instead of stacks.
- The final result = unmatched closing brackets + unmatched opening brackets.

---

## 🏷️ Tags

`String` • `Greedy` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
