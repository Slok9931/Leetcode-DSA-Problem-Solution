# 🔍 Prime Palindrome - LeetCode 866

## 📄 Problem Statement

Find the **smallest prime palindrome** greater than or equal to an integer `n`.

A **prime number** is a number greater than 1 with no positive divisors other than 1 and itself.

A **palindrome** is a number that reads the same forward and backward.

**Return** the smallest prime palindrome ≥ `n`.

🔗 [View on LeetCode](https://leetcode.com/problems/prime-palindrome/)

---

## 🧠 Intuition

- Checking every number ≥ `n` for being both **prime** and **palindromic** would be too slow.
- We can generate palindromes **directly** instead of checking every number.
- All **even-length palindromes > 11** are divisible by 11 and hence not prime, so we only generate **odd-length palindromes**.
- We then check these palindromes for **primality**.

---

## 🛠️ Approach

1. If `n <= 2`, return 2 directly.
2. If `n` is between 8 and 11, return 11 (as even-length palindromes ≥ 11 are not prime).
3. Generate **odd-length palindromes** by:
   - Converting a number `i` to a string.
   - Appending the reverse of `i` (excluding the first digit) to create a palindrome.
   - Example: `i = 123` → `12321`
4. For each such palindrome ≥ `n`, check if it is **prime**.
5. Return the first such number found.

---

## 💻 Code

```cpp
class Solution {
public:
    bool isPrime(int n){
        if(n == 0 || n == 1) return false;
        if(n == 2) return true;
        for(int i=2;i*i<=n;i++){
            if(n % i == 0) return false;
        }
        return true;
    }

    int primePalindrome(int n) {
        if(n <= 2) return 2;
        if(n >= 8 && n <= 11) return 11;

        for(int i = 1; i <= 100000; i++){
            string s = to_string(i);
            string r = s;
            reverse(r.begin(), r.end());
            int x = stoi(s + r.substr(1)); // Generate odd-length palindrome
            if(x >= n && isPrime(x)) return x;
        }

        return 0;
    }
};
```

---

## 🔍 Example

**Input:**  
`n = 13`  

**Output:**  
`101`  

**Explanation:**  
- 13 is not a palindrome.  
- 17, 19, 23... none are palindromes.
- 101 is a palindrome and also prime → ✅  

---

## ⏱️ Time and Space Complexity

| Type | Complexity |
|------|------------|
| 🕒 Time Complexity | O(n * sqrt(n)) (worst case) |
| 🗂 Space Complexity | O(1) |

- We generate up to 100,000 palindromes.  
- For each, we check primality up to `sqrt(n)`.

---

## ✅ Why This Works

- Efficiently **generates palindromes** rather than checking each number.
- Skips all even-length palindromes > 11 which are never prime.
- Primality check is done optimally using `i * i <= n`.

---

## 📌 Key Takeaways

- Clever trick of generating **odd-length palindromes** directly.
- Avoids unnecessary checks for non-palindromes.
- Skips known **non-prime patterns** (even-length palindromes > 11).
- Useful approach for **palindromic number** generation problems in general.

---

## 🏷️ Tags

`Palindrome` • `Prime Numbers` • `Math` • `Optimal Solution` • `LeetCode Medium`

## 🙌 If You Found This Useful
Feel free to ⭐ star this repo or share it with others!
