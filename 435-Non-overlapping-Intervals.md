# 🧹 Non-overlapping Intervals - LeetCode 435

## 📄 Problem Statement

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return the **minimum number of intervals you need to remove** to make the rest of the intervals **non-overlapping**.

> Two intervals that touch at a point (like `[1,2]` and `[2,3]`) are **not** considered overlapping.

🔗 [View on LeetCode](https://leetcode.com/problems/non-overlapping-intervals/)

---

## 🧠 Intuition

- The key to solving this problem is **greedily keeping the interval that ends the earliest**, so that it leaves as much room as possible for upcoming intervals.
- The problem is reduced to: “What’s the maximum number of non-overlapping intervals we can keep?”
- Subtract that number from the total number of intervals to get the **minimum number to remove**.

---

## 🛠️ Approach

1. **Sort the intervals by their end time** (not start time).
2. Initialize a `prev` pointer to the end of the first interval.
3. Iterate over the remaining intervals:
   - If an interval starts **before** `prev`, it **overlaps** → increment the removal counter.
   - Else, update `prev` to the current interval’s end.
4. Return the count of removed intervals.

---

## 💻 Code

```cpp
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        int ans = 0;
        sort(intervals.begin(), intervals.end(), [](const auto& a, const auto& b){
            return a[1] < b[1];
        });
        int prev = intervals[0][1];
        for(int i = 1; i < intervals.size(); i++) {
            if(prev > intervals[i][0]) {
                ans++; // Overlapping, so remove it
            } else {
                prev = intervals[i][1]; // No overlap, update prev
            }
        }
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
`intervals = [[1,2],[2,3],[3,4],[1,3]]` 

**Output:**  
`1`  

**Explanation:**  
- Remove `[1,3]` to make the rest non-overlapping.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n log n) — for sorting |
| 🗂 Space Complexity | O(1) |

---

## ❗ Why Sorting by End Time Works (and Not Start Time)
### ✅ Sorting by end time works because:
- It ensures we always pick the **interval that leaves the most room** for upcoming intervals.
- This greedy choice minimizes removals.

### ❌ Sorting by start time fails:
- Consider this example: `[[1,100],[2,3],[3,4]]`
- Sorting by start time would pick `[1,100]` first, forcing the removal of both `[2,3]` and `[3,4]`.
- But if we sort by end time, we pick `[2,3]` and `[3,4]` — keeping `2` intervals instead of `1`.
This clearly shows that sorting by **end time** leads to a **better optimal solution**.

---

## 📌 Key Takeaways

- Greedy algorithms work well when we make **locally optimal choices** that lead to a global optimum.
- For interval problems, consider sorting by **end time** for optimal overlap control.
- This is a variation of the classic **activity selection problem**.

---

## 🏷️ Tags

`Sorting` • `Greedy` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
