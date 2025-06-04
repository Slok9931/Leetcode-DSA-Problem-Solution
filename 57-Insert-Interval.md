# 📌 Insert Interval - LeetCode 57

## 📄 Problem Statement

You are given an array of **non-overlapping** intervals `intervals` where `intervals[i] = [starti, endi]` represents the start and end of the `i-th` interval. The array is **sorted** in **ascending order** by `starti`.

You are also given another interval `newInterval = [start, end]`.

**Insert** `newInterval` into `intervals` such that:
- The result is still sorted by the start time.
- All overlapping intervals are **merged** into one.

Return the final list of merged, non-overlapping intervals.

🔗 [View on LeetCode](https://leetcode.com/problems/insert-interval)

---

## 🧠 Intuition

We need to insert a new interval into a sorted list and merge overlapping intervals.

The intervals can be categorized into three parts:
1. Intervals completely **before** `newInterval` (no overlap).
2. Intervals that **overlap** with `newInterval`.
3. Intervals completely **after** `newInterval`.

---

## 🛠️ Approach

1. **Add all intervals before `newInterval`** (i.e., whose end is less than the start of `newInterval`).
2. **Merge overlapping intervals**:
   - These intervals satisfy: `intervals[i][0] <= newInterval[1]`.
   - Update `newInterval` to encompass all overlaps.
3. **Add the merged `newInterval`** to the result.
4. **Add remaining intervals** (after `newInterval`).

This way we make only **one pass** through the list and build the result as we go.

---

## 💻 Code

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> ans;
        int i = 0;

        // Step 1: Add all intervals before newInterval
        while (i < intervals.size() && intervals[i][1] < newInterval[0]) {
            ans.push_back(intervals[i]);
            i++;
        }

        // Step 2: Merge overlapping intervals
        while (i < intervals.size() && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
            i++;
        }
        ans.push_back(newInterval); // Add the merged interval

        // Step 3: Add remaining intervals
        while (i < intervals.size()) {
            ans.push_back(intervals[i]);
            i++;
        }

        return ans;
    }
};
```
---

## 🔍 Example

**Input:**  
`intervals = [[1,3],[6,9]], newInterval = [2,5]`  

**Output:**  
`[[1,5],[6,9]]`  

**Explanation:**  
- `[1,3]` overlaps with `[2,5]` → merged into `[1,5]`
- `[6,9]` is after the merged interval, so it remains as-is.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) — Single pass through `intervals` |
| 🗂 Space Complexity | O(n) — For the result array |

---

## ✅ Why This Works

- We handle intervals in **sorted order**, allowing a **linear** solution.
- Merging only happens when necessary (i.e., overlapping intervals).
- We carefully avoid modifying the input and build a clean result.

---

## 📌 Key Takeaways

- This is a classic **merge intervals** problem.
- **Always leverage sorted structure** when it's guaranteed in the input.
- Categorize the input smartly to avoid extra processing.

---

## 🏷️ Tags

`Array` • `Sorting` • `Merge Intervals` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
