# 🍬 Maximum Candies You Can Get from Boxes - LeetCode 1298

## 📄 Problem Statement

You have `n` boxes labeled from `0` to `n - 1`. You are given **four arrays**:

- `status[i]`: `1` if the `i`-th box is open, `0` if it is closed.
- `candies[i]`: number of candies in the `i`-th box.
- `keys[i]`: a list of labels of the boxes you can open after opening the `i`-th box.
- `containedBoxes[i]`: a list of boxes you find inside the `i`-th box.

You are also given an array `initialBoxes` containing the labels of boxes you initially have.

**You can perform the following operations**:

- If a box is open, you can take all the candies inside.
- If the box contains a key to another box, you can now open that box.
- If the box contains other boxes, you can now access those boxes.

**Return** the **maximum number of candies** you can collect by following the rules above.

🔗 [View on LeetCode](https://leetcode.com/problems/maximum-candies-you-can-get-from-boxes)

---

## 🧠 Intuition

- This is a **graph traversal problem** with dependencies.
- We can start from the boxes we already have.
- If a box is **open**, we can explore it immediately.
- If a box is **closed**, we need to find its key first.
- We also need to track boxes and keys we **obtain** while traversing.

---

## 🛠️ Approach

1. Use a **queue** to perform BFS (Breadth-First Search) on boxes.
2. Use boolean arrays to track:
   - `hasBox[i]`: whether we possess box `i`.
   - `hasKey[i]`: whether we possess key to box `i`.
   - `vis[i]`: whether we have already visited box `i`.
3. Initialize the queue with all open boxes from `initialBoxes`.
4. For every box in the queue:
   - If already visited or not open, skip it.
   - Add candies to total.
   - Mark as visited.
   - For each contained box:
     - Mark that we have it.
     - If open, and not visited, add to queue.
   - For each key:
     - Mark that we have the key.
     - Open the corresponding box.
     - If we also have that box and haven't visited it, add to queue.

---

## 💻 Code

```cpp
class Solution {
public:
    int maxCandies(vector<int>& status, vector<int>& candies, vector<vector<int>>& keys, vector<vector<int>>& containedBoxes, vector<int>& initialBoxes) {
        queue<int> q;
        int n = candies.size();
        vector<int> vis(n, false), hasBox(n, false), hasKey(n, false);
        int ans = 0;

        for (int i : initialBoxes) {
            hasBox[i] = true;
            if (status[i]) q.push(i);
        }

        while (!q.empty()) {
            int x = q.front(); q.pop();
            if (vis[x] || !status[x]) continue;

            vis[x] = true;
            ans += candies[x];

            for (int box : containedBoxes[x]) {
                hasBox[box] = true;
                if (status[box] && !vis[box]) q.push(box);
            }

            for (int key : keys[x]) {
                hasKey[key] = true;
                status[key] = true;
                if (hasBox[key] && !vis[key]) q.push(key);
            }
        }

        return ans;
    }
};
```

---

## 🔍 Example

**Input:**  
status = [1,0,1,0], 
candies = [7,5,4,100], 
keys = [[],[],[1],[]], 
containedBoxes = [[1,2],[3],[],[]], 
initialBoxes = [0]  

**Output:**  
16

**Explanation:**  
- Start with box `0` (open): get `7` candies, gain boxes `1`, `2`.
- Box `2` is open: get `4` candies and key to box `1`.
- Use key to open box `1`: get `5` candies and box `3`.
- Box `3` is closed and we don't have key → can't open.
- Total: `7 + 4 + 5 = 16` candies. 

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(N + E) |
| 🗂 Space Complexity | O(N) |

- `N` = total number of boxes
- `E` = total number of elements across `keys` and `containedBoxes`

---

## ✅ Why This Works

This approach ensures:
  - We only process each box once.
  - We never revisit a box.
  - We keep unlocking new boxes using keys and discover more candies efficiently.

---

## 📌 Key Takeaways

- Classic **BFS** with a twist: unlocking and discovering nodes dynamically.
- Managing multiple dependencies (open status, keys, contained boxes).
- Keeping track of what we have and what we can explore.

---

## 🏷️ Tags

`Graph` • `BFS` • `Greedy` • `LeetCode Hard`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
