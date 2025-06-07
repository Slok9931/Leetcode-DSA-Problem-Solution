# 🔍 Minimum Window Substring - Leetcode 76

---

## 📘 Problem Statement

Given two strings `s` and `t`, return the **minimum window substring** of `s` such that every character in `t` (including duplicates) is included in the window.  
If no such substring exists, return the empty string `""`.

**Note:** The answer is guaranteed to be unique.

🔗 [View on Leetcode](https://leetcode.com/problems/minimum-window-substring/)

---

## 🧠 Approach

This problem is solved using the **Sliding Window** technique with a frequency map:

1. Use a frequency array `freq[128]` to store counts of characters in `t`.
2. Expand the right end of the window by iterating through `s`:
   - Decrease the count in the frequency array.
   - If the character was needed, decrease the `count` (number of characters still needed).
3. When `count == 0`, try to shrink the window from the left to find the minimum possible valid window.
4. Track the minimum length and the start index of the window.
5. Return the substring using the saved index and length.

---

## 💻 Code

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        if (s.empty() || t.empty() || s.length() < t.length()) return "";

        vector<int> freq(128, 0);
        for (char c : t) freq[c]++;

        int left = 0, right = 0, count = t.length();
        int minLen = INT_MAX, startIdx = 0;

        while (right < s.size()) {
            if (freq[s[right++]]-- > 0) count--;

            while (count == 0) {
                if (right - left < minLen) {
                    minLen = right - left;
                    startIdx = left;
                }

                if (freq[s[left++]]++ == 0) count++;
            }
        }

        return minLen == INT_MAX ? "" : s.substr(startIdx, minLen);
    }
};
```

---

## 🔍 Example

**Input:**  
```
s = "ADOBECODEBANC"
t = "ABC"
```  

**Output:**  
`"BANC"`  

**Explanation:**  
The substring `"BANC"` contains all characters `A`, `B`, and `C` and is the smallest such substring.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n + m), where `n` is the length of `s` and `m` is the length of `t` |
| 🗂 Space Complexity | O(1), since the frequency array size is constant (128 ASCII characters) |

---

✅ Why This Works
- The **frequency array** tracks how many characters of `t` are still needed.
- The **sliding window** tries to include all characters and then contracts to find the minimum.
- The algorithm ensures **correctness** through character counting and guarantees **minimality** by checking and updating the window size when valid.
  
---

## 📌 Key Takeaways

- Use a **frequency array** to track how many of each character from `t` are needed.
- Expand the right pointer to include characters in the window.
- When the window contains all characters, try to shrink it from the left to find the smallest valid window.
- The **sliding window** technique is powerful for substring problems that require maintaining some condition.
- Count characters carefully to manage duplicates and exact occurrences from `t`.

---

## 🏷️ Tags

`String` • `Sliding window` • `Two-pointer` • `LeetCode Hard`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
