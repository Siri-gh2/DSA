#  Repeated Substring Pattern (KMP / LPS Approach)

## 📌 Problem Link
https://leetcode.com/problems/repeated-substring-pattern/

---

## 🎯 Main Goal

Given a string `s`, determine whether it can be formed by repeating one of its substrings **multiple times**.

### Examples
- `"abab"` → ✅ `("ab" repeated)`
- `"aaaa"` → ✅ `("a" repeated)`
- `"aba"` → ❌
- `"abcabcabc"` → ✅

---

## 🧠 Algorithm Concept: KMP (LPS Array)

This solution uses the **Knuth–Morris–Pratt (KMP)** pattern matching concept — specifically the **LPS (Longest Prefix which is also Suffix)** array.

### What is LPS?
For each index `i`, `lps[i]` stores the length of the **longest proper prefix** of the substring `s[0..i]` that is also a suffix.

---

## 💡 Core Intuition (This Is the Key Insight)

If a string is made by repeating a substring:

- Let `n` = length of string  
- Let `len = lps[n - 1]` (length of longest prefix = suffix)

Then:
- The length of the repeating unit = `n - len`
- If `n % (n - len) == 0`, the string is composed of repeated substrings

### Why this works
- A repeating pattern causes a **self-overlap** in the string
- That overlap is exactly what LPS captures
- No guessing substrings, no brute force — pure structure detection

---

## 🛠️ Approach (Step-by-Step)

1. Initialize an LPS array of size `n`
2. Build the LPS array using standard KMP preprocessing
3. Look at `lps[n-1]`
4. Check:
   - LPS value > 0  
   - `n` is divisible by `(n - lps[n-1])`

If both are true → ✅ repeated pattern exists

---

## ⏱️ Time & Space Complexity

- **Time:** `O(n)`
- **Space:** `O(n)`

Efficient and optimal.

---

## ✅ C++ Implementation (With Comments)

```cpp
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int n = s.size();
        vector<int> lps(n, 0);

        // Build LPS array
        for (int i = 1, j = 0; i < n; ) {
            if (s[i] == s[j]) {
                lps[i++] = ++j;
            } 
            else if (j > 0) {
                j = lps[j - 1];
            } 
            else {
                lps[i++] = 0;
            }
        }

        // Length of longest prefix which is also suffix
        int len = lps[n - 1];

        // Check if string length is divisible by repeating unit length
        return (len > 0) && (n % (n - len) == 0);
    }
};

```
Why This Solution Is Better Than Brute Force:

| Method                   | Time     | Why Not                         |
| ------------------------ | -------- | ------------------------------- |
| Brute substring checking | O(n²)    | Redundant checks                |
| String doubling trick    | O(n)     | Clever but less intuitive       |
| **KMP (this)**           | **O(n)** | Mathematical, scalable, elegant |

**Final Takeaway**

If a string repeats itself, it leaves a footprint —
KMP’s LPS array catches that footprint perfectly.

This is not just a string problem — it’s pattern structure recognition.
