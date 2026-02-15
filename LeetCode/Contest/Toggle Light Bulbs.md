# Toggle Light Bulbs

## Problem
There are 100 light bulbs numbered from **1 to 100**, all initially OFF.

You are given an integer array `bulbs`.  
For every number `b` in the array, toggle the state of bulb `b`.

- If OFF → turn ON  
- If ON → turn OFF  

Return the list of bulbs that remain **ON** in ascending order.

---

## Key Insight

Each occurrence of a bulb number flips its state.

- Appears **odd** times → ON  
- Appears **even** times → OFF  

Because the range is small (1–100), we can store the state in an array instead of using a map or set.

---

## Approach

1. Create a boolean array `on[101]`, initialized to `false`.
2. For each bulb number `b`, flip its value.
3. Traverse from `1` to `100` and collect bulbs that are `true`.

---

## Complexity

- Time: **O(n)**  
- Extra Space: **O(1)** (fixed size array)

---

## Common Mistake ❌

```cpp
on[b] != on[b];
```
This compares, it does NOT update.

So nothing changes.

## Correct Toggle

```
on[b] = !on[b];
```
## C++ Implementation
```
class Solution {
public:
    vector<int> toggleLightBulbs(vector<int>& bulbs) {
        vector<bool> on(101, false);

        for (int b : bulbs) {
            on[b] = !on[b];
        }

        vector<int> res;
        for (int i = 1; i <= 100; i++) {
            if (on[i]) res.push_back(i);
        }

        return res;
    }
};
```

## What I Learned

- Difference between assignment and comparison operators.

- When constraints are small, arrays beat hash maps.

- Tiny syntax mistakes can completely break logic.
