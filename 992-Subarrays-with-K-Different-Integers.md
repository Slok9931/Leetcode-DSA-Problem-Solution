# 📊 Subarrays with K Different Integers - LeetCode 992

## 📄 Problem Statement

Given an integer array `nums` and an integer `k`, return the **number of good subarrays** of `nums`.

A **good subarray** is defined as a contiguous part of the array that contains **exactly `k` different integers**.

> Example:  
> `[1, 2, 1, 2, 3]` has 7 good subarrays with `k = 2`:  
> `[1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,3]`

🔗 [View on LeetCode](https://leetcode.com/problems/subarrays-with-k-different-integers/)

---

## 🧠 Intuition

- This is a classic sliding window problem where we want to count subarrays with **exactly `k` distinct** integers.
- Counting subarrays with **at most `k`** distinct is easier, so we use:
  
  subarraysWithKDistinct = subarrayWithAtMostKDistinct(k) - subarrayWithAtMostKDistinct(k-1)

---

## 🛠️ Approach

1. Implement a helper function to count subarrays with **at most `k`** distinct integers using the sliding window technique and a frequency map.
2. The main function subtracts the result of `at most k-1` from `at most k` to get the count of subarrays with **exactly k** distinct integers.

---

## 💻 Code

```cpp
class Solution {
public:
    int subarrayWithAtmostKDistinct(vector<int>& nums, int k) {
        unordered_map<int, int> freq;
        int left = 0, count = 0, ans = 0;
        for (int right = 0; right < nums.size(); ++right) {
            freq[nums[right]]++;
            if (freq[nums[right]] == 1) count++; // New unique number

            while (count > k) {
                freq[nums[left]]--;
                if (freq[nums[left]] == 0) count--; // One distinct number removed
                left++;
            }

            ans += right - left + 1; // Add all subarrays ending at right
        }
        return ans;
    }

    int subarraysWithKDistinct(vector<int>& nums, int k) {
        return subarrayWithAtmostKDistinct(nums, k) - subarrayWithAtmostKDistinct(nums, k - 1);
    }
};
```

---

## 🔍 Example

**Input:**  
`nums = [1,2,1,2,3], k = 2`  

**Output:**  
`7`  

**Explanation:**  
Subarrays with exactly `2` distinct integers:
`[1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,3]`

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) — Each element is processed at most twice |
| 🗂 Space Complexity | O(n) — For the frequency map |

- Every element is processed at most twice due to the sliding window.

---

## ❓ Why do we compute "At Most K Distinct"?
Because counting **subarrays with exactly `K` distinct integers** directly is hard and inefficient.
But it's **easy and efficient** to count how many subarrays have **at most `K` distinct integers**, using a sliding window.
So, we use this formula:
> Exactly K distinct = At Most K distinct − At Most (K-1) distinct

- **At Most K** includes all subarrays with **1 to K** distinct elements.
- **At Most (K-1)** includes all subarrays with **1 to (K-1)** distinct elements.

So subtracting the second from the first gives **only those subarrays with exactly K distinct**.

---

## 📌 Key Takeaways

- **Sliding Window + Frequency Map** is an effective pattern for handling distinct element counts.
- Rewriting "exactly K" problems as `atMost(K) - atMost(K-1)` is a powerful trick.
- This method avoids recalculating subarrays manually and is scalable to larger constraints.

---

## 🏷️ Tags

`Array` • `Sliding window` • `Two-pointer` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
