# 🔤 Number of Substrings Containing All Three Characters - LeetCode 1358

## 📄 Problem Statement

Given a string `s` consisting only of characters `'a'`, `'b'`, and `'c'`, return the number of **substrings** of `s` that contain **at least one occurrence** of all three characters.

🔗 [View on LeetCode](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters)

---

## 🧠 Intuition

- We need to count **how many substrings** contain **at least one `'a'`, `'b'`, and `'c'`**.
- Instead of generating all substrings (which is inefficient), we use a **sliding window** approach.
- Once a window contains all three characters, all substrings starting at the current `left` and ending from `right` to `end` are valid.

---

## 🛠️ Approach

1. Use two pointers: `left` and `right` to define the window.
2. Maintain counts of `'a'`, `'b'`, and `'c'` in the current window.
3. For every `right`, include `s[right]` in the window.
4. When all three counts are positive:
   - Add `(s.size() - right)` to the answer, because all substrings from `left` to the end are valid.
   - Then shrink the window from `left` to try other possible minimal windows.

---

## 💻 Code

```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
        int a = 0, b = 0, c = 0;
        int left = 0, right, ans = 0;
        for(right = 0; right < s.size(); right++) {
            if(s[right] == 'a') a++;
            else if(s[right] == 'b') b++;
            else if(s[right] == 'c') c++;
            while(a && b && c) {
                ans += s.size() - right;
                if(s[left] == 'a') a--;
                else if(s[left] == 'b') b--;
                else if(s[left] == 'c') c--;
                left++;
            }
        }
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
`s = "abcabc"`  

**Output:**  
`10`  

**Explanation:**  
The substrings that contain at least one `'a'`, `'b'`, and `'c'` are:
- "abc", "abca", "abcab", "abcabc"
- "bca", "bcab", "bcabc"
- "cab", "cabc"
- "abc"

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(1) |

- Every element is processed at most twice due to the sliding window.
- Only constant extra space is used for counters.

---

## ✅ Why This Works

- Once we find a window that contains `'a'`, `'b'`, and `'c'`, every longer substring starting at `left` and ending from `right` to `end` is valid.
- Hence, `s.size() - right` substrings can be counted in `O(1)` time.
- We then move `left` forward to find smaller windows, repeating the process.

---

## 📌 Key Takeaways

- Efficient use of the **sliding window** to count all valid substrings.
- Recognizing that once a condition is met, all larger windows are also valid.
- Good example of combining counting logic with two pointers.

---

## 🏷️ Tags

`String` • `Sliding window` • `Two-pointer` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
