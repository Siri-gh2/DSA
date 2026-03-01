# Minimum Cost to Split into Ones

## 🟡 Problem Summary

You are given an integer `n`.

In one operation:
- Split integer `x` into two positive integers `a` and `b`
- Such that `a + b = x`
- Cost of operation = `a × b`

Return the **minimum total cost** required to split `n` into `n` ones.

---

## 🧠 Key Insight

To minimize cost, always split like this:
```
n → 1 + (n - 1)
```

Why?

Because:
```
1 × (n - 1) < any balanced split
```

Then repeat:
```
n - 1 → 1 + (n - 2)
n - 2 → 1 + (n - 3)
...
```

So total cost becomes:

```
(n - 1) + (n - 2) + (n - 3) + ... + 1
```

That is the sum of first (n-1) natural numbers.

---

## 📐 Formula
```
\[
\frac{n(n - 1)}{2}
\]

---
```
## ✨ Example

### Example 1

Input:
```
n = 3
```

Cost:
```
2 + 1 = 3
```

Output:
```
3
```

---

### Example 2

Input:
```
n = 4

```
Cost:
```
3 + 2 + 1 = 6
```

Output:
```
6
```

---

## 💻 C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    long long minimumCost(int n) {
        return 1LL * n * (n - 1) / 2;
    }
};
```
## ⏱ Complexity

- Time: O(1)

- Space: O(1)
