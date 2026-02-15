# Longest Almost Palindromic Substring

## Problem
Given a string `s`, return the length of the **longest substring** that can become a palindrome after removing **at most one** character.

A substring that is already a palindrome is also valid, because removing any one character will still keep it a palindrome.

---

## Examples

### Example 1
```
Input: s = "zzabba"
Output: 5
```

**Explanation**

Delete one `'z'` → `"zabba"` → palindrome of length **5**.

---

### Example 2
```
Input: s = "abba"
Output: 4
```

Already a palindrome. Removing one character still leaves a palindrome.

---

## Key Insight

Whenever you see:
- substring  
- palindrome  
- longest  

Think 👉 **expand around center**.

While expanding:
1. Move pointers outward as long as characters match.
2. At the first mismatch, we get **one chance**:
   - skip left  
   - skip right  
3. Continue expansion and take the best.

We must check both:
- odd centers → `(i, i)`
- even centers → `(i, i+1)`

---

## Approach

For each index:
- expand normally
- record the pure palindrome
- try skipping one side and continue expansion
- keep the maximum

---

## Complexity

- Time: **O(n²)**
- Space: **O(1)**

Standard for center-expansion palindrome problems.

---

## C++ Solution

```cpp
class Solution {
public:
    int almostPalindromic(string s) {
        int n = s.size();
        int res = 0;

        for (int i = 0; i < n; i++) {
            res = max(res, expandFromCenter(s, i, i));
            res = max(res, expandFromCenter(s, i, i + 1));
        }

        return res;
    }

private:
    int expandFromCenter(const string& s, int l, int r) {
        int n = s.size();

        // Expand normally
        while (l >= 0 && r < n && s[l] == s[r]) {
            l--;
            r++;
        }

        int pure = r - l - 1;

        int option1 = 0, option2 = 0;

        // Skip left
        if (l >= 0) {
            int tl = l - 1, tr = r;
            while (tl >= 0 && tr < n && s[tl] == s[tr]) {
                tl--;
                tr++;
            }
            option1 = tr - tl - 1;
        }

        // Skip right
        if (r < n) {
            int tl = l, tr = r + 1;
            while (tl >= 0 && tr < n && s[tl] == s[tr]) {
                tl--;
                tr++;
            }
            option2 = tr - tl - 1;
        }

        return max({pure, option1, option2});
    }
};
```

## What I Learned

- Center expansion is the first tool for palindrome substring problems.

- Handle both odd and even centers.

- At mismatch → branch once.

- Restarting expansion incorrectly can lose matched length.

## Pattern Tag

Two Pointers • Palindrome • Expand Around Center
