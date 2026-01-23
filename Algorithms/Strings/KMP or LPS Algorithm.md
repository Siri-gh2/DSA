# 🔍 Knuth–Morris–Pratt (KMP) Algorithm

## 📌 Problem
Given a **text** and a **pattern**, find all occurrences of the pattern in the text **efficiently**.

Brute force pattern matching takes **O(n × m)** time in the worst case, which is unacceptable for large strings.

👉 **KMP Algorithm** solves this in **O(n + m)** time.

---

## 🧠 Core Idea (Concept)

KMP avoids **re-checking characters** that are already matched.

Instead of moving the pattern back to the start after a mismatch,  
it uses information from the pattern itself to decide **how much to shift**.

This information is stored in an array called:

### ➤ **LPS Array (Longest Prefix Suffix)**

`lps[i]` = length of the **longest proper prefix** of `pattern[0..i]`
which is also a **suffix** of `pattern[0..i]`.

---

## 🔑 Why LPS Works

When a mismatch occurs:
- We already know some prefix of the pattern matches
- So instead of restarting from scratch,
- We reuse that knowledge using the LPS array

💡 **No character in the text is compared more than once.**

---

## 📖 Example

### Text:

ABABDABACDABABCABAB


### Pattern:


ABABCABAB


---

## 🧮 Step 1: Build LPS Array

Pattern: `A B A B C A B A B`

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|------|---|---|---|---|---|---|---|---|---|
| Char | A | B | A | B | C | A | B | A | B |
| LPS  | 0 | 0 | 1 | 2 | 0 | 1 | 2 | 3 | 4 |

---

## ⚙️ Algorithm Steps

### 1️⃣ Preprocess the pattern
Build the LPS array in **O(m)** time.

### 2️⃣ Pattern Matching
Use two pointers:
- `i` → text
- `j` → pattern

Rules:
- If characters match → move both pointers
- If mismatch:
  - If `j != 0` → `j = lps[j-1]`
  - Else → move `i`

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> computeLPS(string pattern) {
    int m = pattern.length();
    vector<int> lps(m, 0);

    int len = 0; // length of previous longest prefix suffix
    int i = 1;

    while (i < m) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

void KMPSearch(string text, string pattern) {
    int n = text.length();
    int m = pattern.length();

    vector<int> lps = computeLPS(pattern);

    int i = 0; // index for text
    int j = 0; // index for pattern

    while (i < n) {
        if (text[i] == pattern[j]) {
            i++;
            j++;
        }

        if (j == m) {
            cout << "Pattern found at index " << i - j << endl;
            j = lps[j - 1];
        } 
        else if (i < n && text[i] != pattern[j]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i++;
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";

    KMPSearch(text, pattern);
    return 0;
}
```





Dry Run (Key Moments)
Text index i = 10

Characters matched till:
```
ABABC
```

Next mismatch occurs.

Instead of restarting:
```
j = lps[j - 1]

```
Pattern jumps using LPS → no re-checking text characters

Eventually:

Pattern found at index 10

## Time & Space Complexity

| Aspect           | Complexity |
| ---------------- | ---------- |
| LPS construction | O(m)       |
| Pattern search   | O(n)       |
| Total time       | O(n + m)   |
| Extra space      | O(m)       |

## When to Use KMP

✔ Large strings
✔ Multiple pattern searches
✔ Competitive programming
✔ Text editors / search engines

❌ Overkill for very small strings

## Final Takeaway

KMP is not magic.
It’s just smart reuse of previous comparisons.

Once you understand LPS properly,
KMP becomes straightforward — not scary.

## 📌 Practice Tip:
Manually build LPS for at least 5 patterns.
If you skip this, you don’t actually know KMP.

### Happy coding 👩‍💻🔥
