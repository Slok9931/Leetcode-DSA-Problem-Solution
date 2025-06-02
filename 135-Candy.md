# 🍬 Candy Distribution - LeetCode 135 

## 📄 Problem Statement

There are `n` children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subject to the following requirements:

1. Each child must have **at least one** candy.
2. Children with a **higher rating** than their immediate neighbor(s) must get **more candies**.

Return the **minimum number of candies** you need to distribute to satisfy the above conditions.

🔗 [View on LeetCode](https://leetcode.com/problems/candy/)

---

## 🧠 Intuition

We need to reward children based on how their rating compares to their neighbors.

- If ratings are **increasing** (e.g., `1, 2, 3`), each child should get one more candy than the previous.
- If ratings are **decreasing** (e.g., `3, 2, 1`), each child should get fewer candies than the previous (but still at least one).
- If there's a **peak** (a child who is part of both an increasing and decreasing sequence), that child would be counted twice — once from the left and once from the right — so we **subtract the smaller slope** once.

---

## 🛠️ Approach

We use a **greedy one-pass** approach:

1. Start by giving **1 candy to each child** → initialize `ans = n`.
2. Traverse the ratings from left to right using a while loop.
3. For each segment:
   - If the ratings are increasing, count the length of the slope (`up`) and add the sum to `ans`.
   - If the ratings are decreasing, do the same (`down`) and add the sum to `ans`.
4. After both increasing and decreasing slopes, **subtract the overlapping peak** once: `min(up, down)`.
5. Continue this process until the end of the array.
6. Return the final `ans`.

---

## 💻 Code

```cpp
class Solution {
public:
    int candy(vector<int>& ratings) {
        int n = ratings.size();
        int ans = n;
        int i = 1;
        while(i < n){
            if(ratings[i] == ratings[i-1]){
                i++;
                continue;
            }
            int up = 0;
            while(i < n && ratings[i] > ratings[i-1]){
                up++;
                ans += up;
                i++;
            }
            int down = 0;
            while(i < n && ratings[i] < ratings[i-1]){
                down++;
                ans += down;
                i++;
            }
            ans -= min(up, down); // subtract the overlapping peak
        }
        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
`ratings = [1, 0, 2]`  

**Output:**  
`5`  

**Explanation:**  
- Give 2 candies to child 0 (rating 1)  
- 1 candy to child 1 (rating 0)  
- 2 candies to child 2 (rating 2)  

Total candies = `2 + 1 + 2 = 5`

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(1) |

- We traverse the array only once → linear time.  
- Only a few variables are used → constant space.

---

## ✅ Why This Works

- Captures both increasing and decreasing slopes in one pass.
- Subtracts the overlapping peak to avoid double-counting.
- Avoids extra space usage like auxiliary arrays.
- Highly efficient and suitable for large inputs.

---

## 📌 Key Takeaways

- Greedy solution that handles both local increasing and decreasing patterns.
- More optimal than the traditional two-pass method using auxiliary arrays.
- One of the best approaches for interviews and competitive coding rounds.

---

## 🏷️ Tags

`Greedy` • `Array` • `One-pass` • `Optimal Solution` • `LeetCode Hard`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
