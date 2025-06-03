# ✨ Count Number of Nice Subarrays - LeetCode 1248

## 📄 Problem Statement

Given an array of integers `nums` and an integer `k`, return the number of **nice subarrays**.

A **nice subarray** is a **contiguous subarray** that contains **exactly k odd numbers**.

🔗 [View on LeetCode](https://leetcode.com/problems/count-number-of-nice-subarrays)

---

## 🧠 Intuition

- We want to count all **subarrays** with exactly `k` odd numbers.
- Instead of generating all subarrays, we use a **sliding window** and a **clever counting trick**.
- Track the number of valid subarrays ending at each position while maintaining exactly `k` odds.

---

## 🛠️ Approach

1. Use two pointers: `left` and `right` to define a sliding window.
2. Maintain the count of odd numbers in the window (`odd`).
3. When we hit exactly `k` odd numbers:
   - Count how many subarrays end at `right` and still satisfy the condition by sliding `left`.
   - For each valid `left` movement (while still maintaining `k` odd numbers), increase `count`.
4. Add `count` to the final answer `ans`.

---

## 💻 Code

```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        int count = 0, left = 0, right = 0, ans = 0, odd = 0;
        for(right = 0; right < nums.size(); right++) {
            if(nums[right] % 2) {
                odd++;
                count = 0;
            }
            while(odd == k) {
                count++;
                if(nums[left] % 2) odd--;
                left++;
            }
            ans += count;
        }
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
`nums = [1,1,2,1,1], k = 3`  

**Output:**  
`2`  

**Explanation:**  
There are `2` nice subarrays: `[1,1,2,1]` and `[1,2,1,1]`.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(1) |

- Every element is processed at most twice due to the sliding window.

---

## ✅ Why This Works

- For each position with `k` odds in the window, we count how many times we can shift the left pointer while keeping the count the same.
- When a new odd comes in and the window exceeds `k`, we reset and move on.
- This lets us count **all valid subarrays** in a single pass.

---

## 📌 Key Takeaways

- Clever variation of the sliding window pattern.
- Reset `count` every time we get a new odd (as it may open new valid combinations).
- Efficient and clean solution compared to brute-force approaches.

---

## 🏷️ Tags

`Array` • `Sliding window` • `Two-pointer` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
