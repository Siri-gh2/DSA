# Minimum Prefix Removal to Make Array Strictly Increasing

## Problem Statement

You are given an integer array `nums`.

You must remove **exactly one prefix** (possibly empty) from the array such that the **remaining array is strictly increasing**.

Return the **minimum length of the removed prefix**.

A prefix is a subarray that starts from index `0` and ends at any index.

An array is strictly increasing if every element is **strictly greater** than the previous one.

---

## Input Format

- An integer array `nums`

---

## Output Format

- An integer representing the minimum prefix length to remove

---

## Concept

- Greedy strategy  
- Longest strictly increasing suffix  
- Array traversal

---

## Key Idea

After removing a prefix, the remaining array must be a **suffix** of the original array.

So the goal is to find the **longest strictly increasing suffix** and remove everything before it.

---

## Approach

1. Start scanning from the **end of the array**
2. Move left while `nums[i-1] < nums[i]`
3. Stop at the first violation
4. The index where you stop is the prefix length to remove

---

## Example

nums = [1, -1, 2, 3, 3, 4, 5]


### Output

4


---

## Dry Run
```
Start from right:
4 < 5 ✅
3 < 4 ✅
3 < 3 ❌ (stop)

Prefix length = 4


Remaining array:

[3, 4, 5]

Which is strictly increasing.

---

## C++ Code

```cpp
class Solution {
public:
    int minimumPrefixLength(vector<int>& nums) {
        int n = nums.size();
        int i = n - 1;

        while (i > 0 && nums[i - 1] < nums[i]) {
            i--;
        }

        return i;
    }
};

```
### Complexity Analysis

Time Complexity: O(n)

Space Complexity: O(1)

### Takeaway

Think in terms of what must remain, not what to remove.



### Input
