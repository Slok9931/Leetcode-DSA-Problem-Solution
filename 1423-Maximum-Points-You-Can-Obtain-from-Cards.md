# 🃏 Maximum Points You Can Obtain from Cards - LeetCode 1423

## 📄 Problem Statement

There are several cards arranged in a row, and each card has an associated number of points. The points are stored in the integer array `cardPoints`.

You have to take **exactly** `k` cards. In each step, you can pick **one card from the beginning or the end** of the row.

Your **score** is the sum of the points of the selected cards.

**Return the maximum score** you can obtain.

🔗 [View on LeetCode](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards)

---

## 🧠 Intuition

- If we could only take cards from one end, the problem would be simple.
- Since we can choose from both ends, we must try all combinations of taking `i` cards from the front and `k - i` cards from the back for `i` from `0` to `k`.
- Instead of computing every combination separately, we use a **sliding window** trick to optimize.

---

## 🛠️ Approach

1. First, take the first `k` cards and calculate their sum → this is our initial `ans`.
2. Then, slide the window:
   - In each step, remove one card from the end of the `k`-prefix.
   - Add one card from the back of the array.
   - Update the maximum answer.
3. Continue this for `k` steps, always keeping track of the current score and max score.

---

## 💻 Code

```cpp
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int ans = 0;
        for(int i = 0; i < k; i++) ans += cardPoints[i];
        int curr = ans;
        for(int i = k - 1; i >= 0; i--) {
            curr -= cardPoints[i];
            curr += cardPoints[cardPoints.size() - k + i];
            ans = max(ans, curr);
        }
        return ans;
    }
};

```

---

## 🔍 Example

**Input:**  
`cardPoints = [1,2,3,4,5,6,1], k = 3`  

**Output:**  
`2`  

**Explanation:**  
You can pick the cards `[1,2,3]` from the start → sum = 6
Or `[6,1]` from the end and `[1]` from the start → sum = 8
Or `[1,2]` from the start and `[6]` from the end → sum = 9
Or the best: `[1]` from the start and `[6,5]` from the end → sum = 12

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(k) |
| 🗂 Space Complexity | O(1) |

- We only iterate over k elements twice and use constant space for variables.
---

## ✅ Why This Works

- Instead of brute-force evaluating all possible combinations of front/back picks, this method slides a `k`-sized window across both ends efficiently.
- Each update just removes and adds one number — perfect for a sliding window.

---

## 📌 Key Takeaways

- The trick is to **reframe the problem**: instead of picking from both ends randomly, **fix the number of front picks and calculate the rest from the back**.
- Sliding window works efficiently for "**take fixed number of elements**" problems where you can shift contribution between two ends.
- This technique is **better than brute force**, as it avoids redundant recalculations.
- Start with **maximum sum from the front**, then **slide the window toward the back**.

---

## 🏷️ Tags

`Array` • `Sliding window` • `Two-pointer` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
