# Boyer–Moore Algorithm – Efficient Pattern Matching

The **Boyer–Moore Algorithm** is one of the fastest string matching algorithms in practice.

Instead of comparing from left to right like naive methods,  
it compares from **right to left** inside the pattern.

This allows it to skip large portions of the text.

---

## 🧠 Concept Explanation

Given:
- Text `T` of length `n`
- Pattern `P` of length `m`

Traditional algorithms compare from left to right.

Boyer–Moore:
- Aligns pattern with text
- Starts comparison from **last character of pattern**
- On mismatch → shifts pattern smartly

It uses two heuristics:

1. **Bad Character Rule**
2. **Good Suffix Rule**

In most interview implementations, the Bad Character Rule alone is used.

---

## 🔹 1. Bad Character Rule

If mismatch happens at:
   T[i] ≠ P[j]

Shift pattern so that:
- The mismatched character in text aligns
  with its last occurrence in pattern.

If character does not exist in pattern:
- Shift pattern completely past mismatch.

---

### Example

Text:
```
ABAAABCD
```
Pattern:
```
ABC
```

When mismatch occurs at `A`,
pattern jumps ahead instead of shifting by 1.

That’s the power.

---

## 🔹 2. Good Suffix Rule (Advanced)

If a suffix of pattern matches,
but mismatch occurs before it:

Shift pattern to align:
- Another occurrence of that suffix
- Or longest prefix matching that suffix

This gives even larger jumps.

For interviews, Bad Character rule is usually enough.

---

## ⚙️ Approach (Bad Character Version)

1. Preprocess pattern:
   - Store last occurrence of each character

2. Align pattern at start of text

3. Compare from rightmost character

4. If mismatch:
   - Use bad character table to calculate shift

5. Repeat until pattern exceeds text

---

## 🚨 Edge Cases

1. Pattern length > text → no match
2. Empty pattern → always match at index 0
3. Repeated characters
4. Pattern occurs multiple times
5. Character not present in pattern

---

## 💻 C++ Implementation (Bad Character Heuristic)

```cpp
#include <bits/stdc++.h>
using namespace std;

#define NO_OF_CHARS 256

// Preprocessing: bad character heuristic
void badCharHeuristic(string pattern, int m, int badChar[]) {
    for (int i = 0; i < NO_OF_CHARS; i++)
        badChar[i] = -1;

    for (int i = 0; i < m; i++)
        badChar[(int) pattern[i]] = i;
}

// Boyer Moore Search
void search(string text, string pattern) {

    int n = text.length();
    int m = pattern.length();

    if (m == 0) {
        cout << "Empty pattern found at index 0\n";
        return;
    }

    int badChar[NO_OF_CHARS];
    badCharHeuristic(pattern, m, badChar);

    int shift = 0;

    while (shift <= (n - m)) {

        int j = m - 1;

        // Compare from right to left
        while (j >= 0 && pattern[j] == text[shift + j])
            j--;

        // If pattern matches
        if (j < 0) {
            cout << "Pattern found at index " << shift << endl;

            shift += (shift + m < n)
                ? m - badChar[text[shift + m]]
                : 1;
        }
        else {
            shift += max(1, j - badChar[text[shift + j]]);
        }
    }
}

int main() {
    string text = "ABAAABCD";
    string pattern = "ABC";

    search(text, pattern);

    return 0;
}
```
## Complexity Analysis

- Best Case:  O(n / m)

Large jumps when mismatches occur early.

- Average Case: O(n)
- Worst Case: O(n * m)


- Space Complexity: O(1)
  
(256-size array)
