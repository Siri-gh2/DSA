# Maximum Bitwise XOR After Rearrangement

## 🧩 Problem Summary

Given two binary strings:
- `s`
- `t`

You may rearrange characters of `t`.
You cannot modify `s`.

Return the maximum possible XOR string between `s` and rearranged `t`.

---

## 💡 Approach

XOR is `1` when bits differ.

To maximize result:
- If `s[i] == '0'` → prefer using `'1'` from `t`
- If `s[i] == '1'` → prefer using `'0'` from `t`

Count:
- `onesT`
- `zerosT`

Traverse left to right and greedily assign bits to maximize XOR.

---

## ⏱ Complexity

- Time: `O(n)`
- Space: `O(1)`

---

## 💻 C++ Code

```cpp
class Solution {
public:
    string maximumXor(string s, string t) {
        int n = s.size();
        
        int onesT = 0;
        for (char c : t) {
            if (c == '1') onesT++;
        }
        
        int zerosT = n - onesT;
        string result(n, '0');
        
        for (int i = 0; i < n; i++) {
            if (s[i] == '0') {
                if (onesT > 0) {
                    result[i] = '1';
                    onesT--;
                }
            } else {
                if (zerosT > 0) {
                    result[i] = '1';
                    zerosT--;
                }
            }
        }
        
        return result;
    }
};

```

## 🧠 What I Understood

- We are allowed to rearrange string `t`, but not `s`.
- XOR gives 1 when bits are different.
- So to maximize XOR:
  - If s[i] = 0 → try to place 1 from t.
  - If s[i] = 1 → try to place 0 from t.
- We don’t need to actually build rearranged `t`.
- We only need to count how many 0s and 1s are in `t`.
- Then greedily assign bits to maximize XOR from left to right.
- Since higher bits matter more, greedy works.
- This is a counting + greedy problem, not a bit manipulation trick problem.
