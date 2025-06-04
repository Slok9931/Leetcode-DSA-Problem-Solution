# 🌸 Minimum Number of Days to Make m Bouquets - LeetCode 1482

## 📄 Problem Statement

You are given an integer array `bloomDay`, and two integers `m` and `k`.

- You want to make **`m` bouquets**.
- Each bouquet must consist of **`k` adjacent flowers**.
- The `i-th` flower blooms on `bloomDay[i]` and can be used **only once**.

**Return** the **minimum number of days** required to make `m` bouquets.  
If it’s impossible to make `m` bouquets, return `-1`.

🔗 [View on LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets)

---

## 🧠 Intuition

- The more days you wait, the more flowers will bloom — and the easier it will be to make bouquets.
- Once a day is found where it's possible to make `m` bouquets, any day **after** that will also work.
- This **monotonic condition** makes it a great candidate for **binary search**.

---

## 🛠️ Approach

1. **Edge Case**: If `m * k > bloomDay.size()`, it is **impossible** to make `m` bouquets. Return `-1`.
2. Set the **search space** from `1` to `maxi` (the max possible bloom day).
3. For each `mid` day in binary search:
   - Use a helper `isPossible()` function to check if `m` bouquets can be made by that day.
4. If it’s possible, try fewer days (`e = mid`).
5. If it’s not possible, try more days (`s = mid + 1`).
6. The first day where it’s possible is the **minimum**.

---

## 💻 Code

```cpp
class Solution {
public:
    int minDays(vector<int>& bloomDay, int m, int k) {
        if((long long)m*k > bloomDay.size()) return -1;
        int maxi = 1;
        for(int i=0;i<bloomDay.size();i++) maxi = max(maxi, bloomDay[i]);
        int s = 1, e = maxi;
        while(s < e){
            int mid = s + (e-s)/2;
            if(isPossible(bloomDay, m, k, mid)) e = mid;
            else s = mid + 1;
        }
        return s;
    }
private:
    bool isPossible(vector<int>& bloomDay, int m, int k, int day){
        int total = 0;
        for(int i=0;i<bloomDay.size();i++){
            int count = 0;
            while(i < bloomDay.size() && count < k && bloomDay[i] <= day){
                count++;
                i++;
            }
            if(count == k){
                total++;
                i--;
            }
            if(total >= m) return true;
        }
        return false;
    }
};
```
---

## 🔍 Example

**Input:**  
`bloomDay = [1,10,3,10,2], m = 3, k = 1`  

**Output:**  
`3`  

**Explanation:**  
On day `3`, the flowers at indices `0`, `2`, and `4` are bloomed.
They can be used to form `3` bouquets of `1` flower each.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n * log(max bloomDay)) |
| 🗂 Space Complexity | O(1) |

- Binary search runs in `log(max bloomDay)` time.
- For each `mid`, we scan the array once to check feasibility → `O(n)`.
---

## ✅ Why This Works

- The number of bouquets that can be formed is a **non-decreasing function** of time.
- This means we can use **binary search** over the number of days to find the minimum viable day.

---

## 📌 Key Takeaways

- If a problem asks for the **minimum or maximum possible** value under a **monotonic condition**, try **binary search on answer space**.
- In integer math, always handle `mid = s + (e - s) / 2` to avoid overflow.
- Double-check edge cases like when total flowers are insufficient: `m * k > n`.

---

## 🏷️ Tags

`Greedy` • `Array` • `Binary Search` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
