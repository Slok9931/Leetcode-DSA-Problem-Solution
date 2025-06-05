# 🔤 Lexicographically Smallest Equivalent String - LeetCode 1061

## 📄 Problem Statement

You are given two strings `s1` and `s2` of **equal length** and a string `baseStr`.

Characters `s1[i]` and `s2[i]` are declared **equivalent**, forming equivalency relations.

Your task is to:

🔹 Use the equivalency information from `s1` and `s2`  
🔹 Transform `baseStr` into its **lexicographically smallest equivalent string**

Two characters are considered **equivalent** if they are:
- **Reflexive**: `'a' == 'a'`
- **Symmetric**: `'a' == 'b'` ⇒ `'b' == 'a'`
- **Transitive**: `'a' == 'b'` and `'b' == 'c'` ⇒ `'a' == 'c'`

Return the **lexicographically smallest** string possible using the equivalency mapping.

🔗 [View on LeetCode](https://leetcode.com/problems/lexicographically-smallest-equivalent-string)

---

## 🧠 Intuition

This is a **Union-Find (Disjoint Set Union)** problem.

We model each character as a node. If two characters are equivalent, we join their sets.

To ensure **lexicographically smallest** characters dominate:
- Always point the higher character to the smaller one when performing union.

---

## 🛠️ Approach

1. Initialize a parent array `mp` of size 26 (for characters `'a'` to `'z'`).
2. Union characters from `s1` and `s2`, ensuring the **lexicographically smaller** character becomes the representative (root).
3. For every character in `baseStr`, find the **root representative**.
4. Replace each character in `baseStr` with its **smallest equivalent character**.

---

## 💻 Code

```cpp
class Solution {
    int Find_root(int n, vector<int> &mp) {   
        if (mp[n] == n)
            return n;     
        return Find_root(mp[n], mp);
    }
public:
    string smallestEquivalentString(string s1, string s2, string baseStr) {
        vector<int> mp(26);
        for (int i = 0; i < 26; i++) {
            mp[i] = i;
        }

        for (int i = 0; i < s1.length(); i++) {  
            int r1 = Find_root(s1[i] - 'a', mp);    
            int r2 = Find_root(s2[i] - 'a', mp); 
            if (r1 < r2) {
                mp[r2] = r1;
            } else {
                mp[r1] = r2;
            }          
        }

        for (auto &ch : baseStr) {
            char c = ch;
            while (c != mp[c - 'a'] + 'a') {
                c = mp[c - 'a'] + 'a';
            }
            ch = c;
        }

        return baseStr;
    }
};
```

---

## 🔍 Example

**Input:**  
```
s1 = "parker"
s2 = "morris"
baseStr = "parser"
``` 

**Output:**  
`"makkek"`  

**Explanation:**  
- From the mappings:
  `p==m, a==o, r==r, k==i, e==s`
- Replace each letter with the lexicographically smallest in its equivalence class.

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n * α(26)) where α is inverse Ackermann function (near constant) |
| 🗂 Space Complexity | O(1) |

- Every element is processed at most twice due to the sliding window.

---

## ✅ Why This Works

- Union-Find allows us to manage equivalence efficiently.
- By always choosing the **smallest lexicographical** character as the parent during union, we ensure the output is **minimal**.
- Finding the representative character lets us standardize each equivalence class.

---

## 📌 Key Takeaways

- Union-Find is a powerful tool for modeling equivalence.
- Always choose **lexicographically smallest** elements as roots when the result requires ordering.
- This technique generalizes well to string normalization problems.

---

## 🏷️ Tags

`Union Find` • `Graph` • `String` • `Greedy` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
