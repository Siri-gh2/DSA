# Naive String Matching Algorithm

The **Naive String Matching Algorithm** is the simplest method
to find occurrences of a pattern inside a text.

It checks for a match at every possible position.

---

## 🧠 Concept Explanation

Given:
- Text `T` of length `n`
- Pattern `P` of length `m`

We try to match `P` with every substring of `T`
of length `m`.

For each possible starting index `i`:
- Compare `T[i + j]` with `P[j]`
- If all characters match → pattern found
- If mismatch → shift pattern by 1

It is called “naive” because it does not reuse
any previous comparisons.

---

## 📌 Example

Text:
```
AABAACAADAABAABA
```

Pattern:
```
AABA
```

We check:

- Start at index 0 → match ✔
- Start at index 1 → mismatch
- Start at index 2 → mismatch
- ...
- Continue until end

---

## ⚙️ Approach

1. Let `n = text.length()`
2. Let `m = pattern.length()`
3. For `i = 0` to `n - m`:
   - Compare characters one by one
   - If all `m` characters match → report match

---

## 🚨 Edge Cases

1. Pattern length > text → no match
2. Empty pattern → always match at index 0
3. Pattern equals text → one match
4. Repeated characters
5. Multiple occurrences allowed

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

void naiveSearch(string text, string pattern) {

    int n = text.length();
    int m = pattern.length();

    if (m == 0) {
        cout << "Empty pattern found at index 0\n";
        return;
    }

    if (m > n) {
        cout << "Pattern longer than text. No match.\n";
        return;
    }

    for (int i = 0; i <= n - m; i++) {

        int j;

        for (j = 0; j < m; j++) {
            if (text[i + j] != pattern[j])
                break;
        }

        if (j == m) {
            cout << "Pattern found at index " << i << endl;
        }
    }
}

int main() {

    string text = "AABAACAADAABAABA";
    string pattern = "AABA";

    naiveSearch(text, pattern);

    return 0;
}
```
## ⏱ Complexity Analysis
- Worst Case:  O(n * m)

Example worst case:
Text = "AAAAAA"
Pattern = "AAA"

Many repeated comparisons occur.

- Best Case:  O(n)

If mismatch occurs at first character every time.

- Space Complexity: O(1)

No extra data structures used.
