# 📏 Minimum Size Subarray Sum - LeetCode 209

## 📄 Problem Statement

Given an array of **positive integers** `nums` and a positive integer `target`, return the **minimal length** of a **contiguous subarray** of which the sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

🔗 [View on LeetCode](https://leetcode.com/problems/minimum-size-subarray-sum)

---

## 🧠 Intuition

- We need the **shortest subarray** with a sum **≥ target**.
- Since all numbers are **positive**, we can apply the **sliding window** technique efficiently.
- If current window sum ≥ target, shrink the window from the left to try for a smaller size.

---

## 🛠️ Approach

1. Initialize two pointers: `left` and `right` for the sliding window.
2. Move `right` to extend the window, adding `nums[right]` to the current sum.
3. When the sum becomes ≥ target:
   - Update the minimum length `ans`.
   - Move `left` pointer to reduce the window size while maintaining the required sum.
4. If no valid window is found, return `0`.

---

## 💻 Code

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0, right = 0, ans = nums.size();
        int sum = 0;
        for(int i = 0; i < nums.size(); i++) sum += nums[i];
        if(sum < target) return 0;
        sum = 0;
        for(right = 0; right < nums.size(); right++) {
            sum += nums[right];
            if(sum >= target) ans = min(ans, right - left + 1);
            while(sum >= target) {
                sum -= nums[left];
                left++;
                if(sum >= target) ans = min(ans, right - left + 1);
            }
        }
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
```
target = 7
nums = [2,3,1,2,4,3]
```  

**Output:**  
`2`  

**Explanation:**  
The subarray `[4,3]` has the minimal length under the problem constraint.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(1) |

- Each element is visited at most twice: once by `right`, once by `left`.

---

## ✅ Why This Works

- Uses the **sliding window** pattern for optimal linear-time performance.
- Shrinks the window only after the sum condition is met.
- Ensures we get the **smallest valid window**.

---

## 📌 Key Takeaways

- Ideal use case for **two-pointer / sliding window** approach.
- Always track the current minimum length as soon as the window becomes valid.
- Avoid brute-force which would lead to O(n²) time.

---

## 🏷️ Tags

`Array` • `Sliding window` • `Two pointer` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
