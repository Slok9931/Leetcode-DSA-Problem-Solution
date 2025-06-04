# 🎲 Find the Lexicographically Largest string from the Box - Leetcode 3403

## 📄 Problem Statement

You are given:
- A string `word`
- An integer `numFriends`

Alice is organizing a game with her `numFriends`. In each round:
1. She splits `word` into `numFriends` non-empty parts such that no previous round has had the same exact split.
2. All the parts from each split are placed into a **box**.
3. After all possible unique splits, the **lexicographically largest string** among all strings in the box is the result.

🧩 You need to return **that lexicographically largest string** from the box.

🔗 [View on LeetCode](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-i)

---

## 🧠 Intuition

The total number of possible unique splits can be large and generating all of them is inefficient.  
Instead, we want to **find the optimal substring** that:
- Could be one of the parts of a valid split.
- Will **maximize the lexicographical order**.

This is essentially about finding a **starting index `i`** in the string such that the substring `word[i]` is lexicographically the greatest possible **within the allowed length** (`n - numFriends + 1`).

---

## 🛠️ Approach

1. If `numFriends == 1`, return the whole string (only one piece allowed).
2. Initialize two pointers:  
   - `i` = candidate starting index  
   - `j` = current character to compare with `i`
3. Move `j` forward while comparing characters at `i + k` and `j + k` (where `k` is the offset).
4. If substring starting at `j` is better, update `i = j`.
5. Finally, return substring from `i` of length `min(n - i, n - numFriends + 1)`.

---

## 💻 Code

```cpp
class Solution {
public:
    string answerString(string word, int numFriends) {
        int n = word.size(), i = 0, j = 1;
        if(numFriends == 1) return word;
        while(j < n){
            while(j < n && word[i] > word[j]) j++;
            if(j < n && word[i] < word[j]) i = j;
            else{
                int k = 0;
                while(j + k < n && word[i + k] == word[j + k]) k++;
                if(j + k < n && word[i + k] < word[j + k]) i = j;
            }
            j++;
        }
        return word.substr(i, min(n - i, n - numFriends + 1));
    }
};

```

---

## 🔍 Example

**Input:**  
`word = "abcabc", numFriends = 3`  

**Output:**  
`"cabc"`  

**Explanation:**  
Possible splits include:
- ("a", "b", "cabc")
- ("abc", "a", "bc")
- ...
All substrings from splits are collected.
Among all substrings, `"cabc"` is lexicographically largest.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n) |
| 🗂 Space Complexity | O(1) |

- We traverse the string only once → linear time.  
- Only a few variables are used → constant space.

---

## ✅ Why This Works

The key observation is:
- In every valid split into `numFriends` parts, at least **one of the substrings** will have length ≤ `n - numFriends + 1`.
- The lexicographically largest such substring will **definitely** appear in one of the splits.
- So, we can find the **starting index `i`** such that `word[i]` is the largest, and return `word.substr(i, n - numFriends + 1)`.

To efficiently find the best starting index:
- We iterate over the string using two pointers (`i` and `j`) to compare substrings.
- This is similar to Duval’s algorithm (used in Lyndon factorization).

---

## 📌 Key Takeaways

- Instead of generating all split combinations, you can **strategically find** the lexicographically largest candidate substring.
- This is a variation of Lyndon word and **Duval's algorithm** for minimal string rotations.
- Great example of how **greedy and two-pointer** techniques can optimize seemingly brute-force problems.

---

## 🏷️ Tags

`Greedy` • `String` • `Two pointer` • `Lyndon Factorization` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
