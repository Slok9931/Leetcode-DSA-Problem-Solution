# 🔄 Merge Intervals - LeetCode 56

## 📄 Problem Statement

You are given an array of intervals where `intervals[i] = [starti, endi]`. Merge all overlapping intervals and return **an array of the non-overlapping intervals** that cover all the intervals in the input.

> Two intervals `[a, b]` and `[c, d]` overlap if `c <= b` and `a <= d`.

🔗 [View on LeetCode](https://leetcode.com/problems/merge-intervals/)

---

## 🧠 Intuition

- If we **sort** the intervals by their start time, then any overlapping intervals will be **adjacent** in the sorted list.
- We can scan through the sorted list and merge intervals whenever there's an overlap.
- This is a classic greedy + sorting problem.

---

## 🛠️ Approach

1. **Sort** the intervals by their starting point.
2. Initialize a `prev` interval to the first interval.
3. Iterate over the rest of the intervals:
   - If the current interval **overlaps** with `prev` (i.e., `intervals[i][0] <= prev[1]`), merge them.
   - Otherwise, push `prev` to the result and update `prev` to the current interval.
4. Add the last `prev` interval to the result.

---

## 💻 Code

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        vector<int> prev = intervals[0];
        for(int i = 1; i < intervals.size(); i++) {
            if(intervals[i][0] <= prev[1]) {
                prev[1] = max(prev[1], intervals[i][1]); // Merge
            } else {
                ans.push_back(prev); // No overlap, add previous
                prev = intervals[i];
            }
        }
        ans.push_back(prev); // Push the last interval
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
`intervals = [[1,3],[2,6],[8,10],[15,18]]` 

**Output:**  
`[[1,6],[8,10],[15,18]]`  

**Explanation:**  
- [1,3] and [2,6] overlap → merged to [1,6]
- [8,10] and [15,18] do not overlap.
---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n log n) — due to sorting |
| 🗂 Space Complexity | O(n) — for the output list |

---

## ✅ Why This Works

- Sorting ensures that overlapping intervals are grouped.
- We only need to track the **current merged interval**, which makes the algorithm efficient and clean.

---

## 📌 Key Takeaways

- Always **sort intervals by start time** when merging or checking overlap.
- Use a greedy merge strategy when two intervals overlap.
- This problem appears often in real-world scheduling and merging use cases.

---

## 🏷️ Tags

`Sorting` • `Greedy` • `Array` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
