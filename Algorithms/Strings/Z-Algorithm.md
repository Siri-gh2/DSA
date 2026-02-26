# Z-Algorithm (Z-Function) – String Pattern Matching

The **Z-Algorithm** is a linear time string matching algorithm.

It computes a `Z-array` where:

`Z[i] = length of the longest substring starting from index i`
that matches the prefix of the string.

---

## 🧠 Concept Explanation

For a string `s` of length `n`:

- `Z[0]` is usually defined as `0`
- For every `i > 0`,
  `Z[i]` tells how many characters from `s[i...]`
  match with the prefix `s[0...]`

### Example

For:
s = "aabcaabxaaaz"

Z-array becomes:
```
[0,1,0,0,3,1,0,0,2,1,0,0]
```

Meaning:
- At index 4 → substring "aabxaaaz"
  matches prefix "aab" → length = 3

---

## 🔎 Why Z-Algorithm is Important?

It is used for:

- Pattern matching in O(n)
- Finding repeated substrings
- Finding string periodicity
- Solving many competitive programming problems

---

## ⚙️ Approach

Instead of matching from scratch at every index,
we maintain a window `[L, R]`:

- `[L, R]` represents the current segment
  which matches with the prefix.
- We reuse previous computations
  to avoid unnecessary comparisons.

### Steps:

1. Initialize:
       L = 0, R = 0
2. Traverse from `i = 1` to `n-1`
3. If `i > R`
- Start fresh comparison
- Update L and R
4. Else (`i <= R`)
- Use previously computed values
- Try extending match beyond R
5. Continue until end

This ensures linear time complexity.

---

## 🚨 Edge Cases

1. Empty string → return empty Z-array
2. Single character string → `[0]`
3. All characters same → worst expansion but still O(n)
4. No repeated prefix → mostly zeros
5. Pattern matching case:
When using for pattern matching:
```
bool patternExists(string text, string pattern) {
    string combined = pattern + "$" + text;
    vector<int> Z = computeZ(combined);

    int pLen = pattern.length();

    for (int i = 0; i < Z.size(); i++) {
        if (Z[i] == pLen)
            return true;
    }

    return false;
}
```
## Complexity Analysis
- Time Complexity: O(N)
- Space Complexity : O(N)

