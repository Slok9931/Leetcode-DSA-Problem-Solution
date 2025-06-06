# 🤖 Lexicographically Smallest String After Operations With String - LeetCode 2434

## 📄 Problem Statement

You are given a string `s` and a robot that holds an initially empty string `t`. The robot can perform the following operations **any number of times** until both `s` and `t` are empty:

1. **Take Operation**: Remove the **first character** of string `s` and **append** it to the end of `t`.
2. **Write Operation**: Remove the **last character** of string `t` and **write** it on paper (i.e., append it to the output string).

Your goal is to return the **lexicographically smallest string** that can be written on paper by applying these operations optimally.

🔗 [View on LeetCode](https://leetcode.com/problems/lexicographically-smallest-string-after-operations-with-constraint/)

---

## 🧠 Intuition

We need to output characters in **lexicographically smallest** order using the two operations allowed.

### Observations:

- You **must** process the string `s` from **left to right**.
- You can **delay outputting characters** from `t` until they help create a smaller result.
- Therefore, we need to keep `t` in a stack-like structure, and greedily write the top character if it's the smallest possible going forward.

---

## 🛠️ Approach

1. Precompute a suffix array `min_suffix[i]` such that it stores the **minimum character** in the suffix of `s` starting from index `i`.
2. Use a string `t` to simulate the robot's holding string.
3. For each character in `s`:
   - Push it into `t`.
   - While the last character in `t` is **less than or equal** to the **minimum upcoming character**, pop from `t` and write it to the result.
4. Return the result.

---

## 💻 Code

```cpp
class Solution {
public:
    string robotWithString(string s) {
        int n = s.size();
        string result, t;
        vector<char> min_suffix(n);
        min_suffix[n - 1] = s[n - 1];
        for (int i = n - 2; i >= 0; --i)
            min_suffix[i] = min(s[i], min_suffix[i + 1]);
        for (int i = 0; i < n; ++i) {
            t.push_back(s[i]);
            while (!t.empty() && (i == n - 1 || t.back() <= min_suffix[i + 1])) {
                result += t.back();
                t.pop_back();
            }
        }
        return result;
    }
};
```

---

## 🔍 Example

**Input:**  
`s = "zza"` 

**Output:**  
`"azz"`  

**Explanation:**  
- Step 1: Move 'z' to t → t = "z"
- Step 2: Move 'z' to t → t = "zz"
- Step 3: Move 'a' to t → t = "zza"
- Step 4: 'a' is the smallest, write it → result = "a", t = "zz"
- Step 5: write 'z', result = "az"
- Step 6: write 'z', result = "azz"

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) — One pass for suffix min array, one pass for the main logic |
| 🗂 Space Complexity | O(n) — For suffix array and robot's stack `(t)` |

- Every element is processed at most twice due to the sliding window.

---

## ✅ Why This Works

- By always checking whether the top of `t` is less than or equal to any future character, we ensure the **greedy lexicographical order**. We don’t delay writing characters that won’t be beaten later.
---

## 📌 Key Takeaways

- Precomputing minimum suffix characters helps us make greedy decisions.
- Stack-like behavior of the robot `(t)` makes it efficient.
- Lexicographical problems often benefit from combining **greedy + auxiliary arrays**.

---

## 🏷️ Tags

`Lexicographical Order` • `String` • `Greedy` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
