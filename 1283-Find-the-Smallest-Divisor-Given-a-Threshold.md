# 📉 Find the Smallest Divisor Given a Threshold - LeetCode 1283

## 📄 Problem Statement

Given an array of integers `nums` and an integer `threshold`, find the **smallest positive integer divisor** such that the **sum of all division results** is **less than or equal to** the threshold.

> Each result of the division is **rounded up** to the nearest integer.  
> For example:  
> - `7 / 3 = 3`  
> - `10 / 2 = 5`  
> - `1 / 10 = 1`

The test cases are guaranteed to have a solution.

🔗 [View on LeetCode](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold)

---

## 🧠 Intuition

- The **larger the divisor**, the **smaller the sum**.
- This is a **monotonic function** — as the divisor increases, the total sum strictly decreases.
- That’s a good sign to apply **binary search** on the divisor itself.

---

## 🛠️ Approach

1. The smallest possible divisor is `1`.
2. The largest possible divisor is `max(nums)` because anything larger would make the whole array result in `1`s.
3. Use **binary search** on the divisor range:
   - For each `mid` (candidate divisor), compute the sum of `ceil(nums[i] / mid)` for all `i`.
   - If the sum is **≤ threshold**, try to reduce the divisor.
   - If the sum is **> threshold**, increase the divisor.
4. Return the **smallest** divisor that satisfies the condition.

---

## 💻 Code

```cpp
class Solution {
public:
    int smallestDivisor(vector<int>& nums, int threshold) {
        int maxi = INT_MIN;
        for(int i = 0; i < nums.size(); i++) maxi = max(maxi, nums[i]);
        int s = 1, e = maxi;
        int ans = INT_MAX;
        while(s <= e) {
            int mid = s + (e - s) / 2;
            int sum = 0;
            for(int i = 0; i < nums.size(); i++) {
                sum += (nums[i] + mid - 1) / mid; // Equivalent to ceil(nums[i]/mid)
            }
            if(sum <= threshold) {
                ans = min(ans, mid);
                e = mid - 1;
            } else {
                s = mid + 1;
            }
        }
        return ans;
    }
};

```

---

## 🔍 Example

**Input:**  
`nums = [1,2,5,9], threshold = 6`  

**Output:**  
`5`  

**Explanation:**  
Try divisors:
- `1 → 1+2+5+9 = 17` ❌
- `2 → 1+1+3+5 = 10` ❌
- `5 → 1+1+1+2 = 5` ✅ meets the condition

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n * log(max(nums))) |
| 🗂 Space Complexity | O(1) |

---

## ✅ Why This Works

We apply binary search over the possible **divisor values** from `1` to `max(nums)`.

- For each possible divisor `d`, we calculate the total sum:  
  `sum = ceil(nums[0]/d) + ceil(nums[1]/d) + ... + ceil(nums[n-1]/d)`
- If this sum is **≤ threshold**, then we try smaller divisors (`e = mid - 1`) to minimize.
- If the sum is **> threshold**, we must increase the divisor (`s = mid + 1`).

This works because the function `f(divisor) = total sum` is **monotonically decreasing**, which is the ideal condition for binary search.

---

## 📌 Key Takeaways

- If you can convert a problem to a **monotonic condition**, you can usually apply **binary search** efficiently.
- Use the trick: `ceil(a/b) = (a + b - 1) / b` in integer math.
- Binary search isn’t just for arrays—it works great on **answer spaces** when the function is monotonic.



---

## 🏷️ Tags

`Greedy` • `Array` • `Binary Search` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
