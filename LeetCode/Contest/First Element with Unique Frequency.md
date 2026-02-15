# First Element with Unique Frequency

## Problem
Given an integer array `nums`, return the **first element (from left to right)** whose frequency is **unique**.

A frequency is unique if **no other number** appears the same number of times.

If no such element exists, return `-1`.

---

## Key Understanding

This is **NOT** asking for:

❌ first element that appears once  
❌ first element with frequency > 1  

It is asking for:

✅ the first element whose **repetition count** is different from every other number’s repetition count.

---

## Example
```
nums = [20, 10, 30, 30]
```

### Step 1 → Count each number
```

20 → 1
10 → 1
30 → 2
```

### Step 2 → Count the frequencies

```
1 → 2 numbers
2 → 1 number
```

### Step 3 → Scan from left
- 20 → freq = 1 → not unique ❌  
- 10 → freq = 1 → not unique ❌  
- 30 → freq = 2 → unique ✅  

Answer = **30**

---

## Approach

We need **two hash maps**.

### Map 1
number → frequency


### Map 2

frequency → how many numbers have this frequency


Then scan the array from left to right and return the first number whose frequency count is `1`.

---

## Why scan the array again?

Because we must return the **first in order**, not random from the map.

---

## Complexity
```
- Time: **O(n)**
- Space: **O(n)**
```
Optimal.

---

## C++ Implementation

```cpp
class Solution {
public:
    int firstUniqueFreq(vector<int>& nums) {
        unordered_map<int,int> freq;

        for(int x : nums) freq[x]++;

        unordered_map<int,int> count;
        for(auto &p : freq) count[p.second]++;

        for(int x : nums)
        {
            if(count[freq[x]] == 1) return x;
        }

        return -1;
    }
};
```
## What I Learned

- Some problems require counting values and then counting the counts.

- Order matters → scan original array at the end.

- “Unique element” and “unique frequency” are completely different ideas.
