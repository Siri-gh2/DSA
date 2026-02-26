# Manacher’s Algorithm – Longest Palindromic Substring in O(n)

Manacher’s Algorithm is a linear time algorithm used to find:

- Longest Palindromic Substring
- All palindromic substrings

Unlike brute force (O(n³)) or center expansion (O(n²)),  
Manacher runs in **O(n)** time.

---

## 🧠 Concept Explanation

The key difficulty in palindrome problems:

- Even length palindromes (abba)
- Odd length palindromes (aba)

Manacher solves this by:

👉 Transforming the string to avoid separate handling.

---

## 🔄 String Transformation

We insert a special character `#` between every character.

Example:

Original:
  ```
abba
```
Transformed:
```
^#a#b#b#a#$
```

Why add `^` and `$`?
- To prevent out-of-bound checks
- Acts as sentinels

Now:
- Every palindrome becomes odd-length
- No need to handle even/odd separately

---

## 📌 Core Idea

We maintain:

- `center` → center of current palindrome
- `right` → right boundary of that palindrome

For every index `i`:

1. Find mirror index:
       mirror = 2*center - i
   
2. If `i < right`:
   
       P[i] = min(right - i, P[mirror])

3. Try expanding around `i`

4. If palindrome expands beyond `right`,
update `center` and `right`

This reuse of mirror information gives O(n) time.

---

## 🚨 Edge Cases

1. Empty string → return ""
2. Single character → itself is palindrome
3. All characters same → entire string is palindrome
4. No repeating characters → answer is any single character
5. Even-length palindrome handled automatically after transformation

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

string longestPalindrome(string s) {

 if (s.empty()) return "";

 // Step 1: Transform string
 string t = "^";
 for (char c : s) {
     t += "#" + string(1, c);
 }
 t += "#$";

 int n = t.length();
 vector<int> P(n, 0);

 int center = 0, right = 0;

 for (int i = 1; i < n - 1; i++) {

     int mirror = 2 * center - i;

     if (i < right)
         P[i] = min(right - i, P[mirror]);

     // Expand around center i
     while (t[i + (1 + P[i])] == t[i - (1 + P[i])]) {
         P[i]++;
     }

     // Update center and right boundary
     if (i + P[i] > right) {
         center = i;
         right = i + P[i];
     }
 }

 // Find maximum palindrome length
 int maxLen = 0;
 int centerIndex = 0;

 for (int i = 1; i < n - 1; i++) {
     if (P[i] > maxLen) {
         maxLen = P[i];
         centerIndex = i;
     }
 }

 int start = (centerIndex - maxLen) / 2;

 return s.substr(start, maxLen);
}

int main() {
 string s = "babad";
 cout << longestPalindrome(s);
 return 0;
}
```
## Complexity Analysis:
Time Complexity : O(N)
Space Complexity : O(N)
