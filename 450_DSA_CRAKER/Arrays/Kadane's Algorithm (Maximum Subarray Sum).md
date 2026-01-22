# Kadane’s Algorithm – Maximum Subarray Sum

This problem focuses on finding the **maximum sum of a contiguous subarray** within a given array.  
It is one of the most **important array problems** and a classic example of **dynamic programming with optimization**.

---

## 📌 Problem Links
- [GeeksforGeeks – Kadane’s Algorithm](https://www.geeksforgeeks.org/problems/kadanes-algorithm-1587115620/1)
- [Code360 – Maximum Subarray Sum](https://www.naukri.com/code360/problems/maximum-subarray-sum_630526?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker)

---

## 🧠 Concept

Given an array of integers (which may include negative numbers), the task is to find the **maximum possible sum of a contiguous subarray**.

Example:
Input : [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output : 6
Explanation : Subarray [4, -1, 2, 1] has the maximum sum = 6


The brute-force approach checks all subarrays, but Kadane’s Algorithm optimizes this to **linear time**.

---

## 📐 Approach (Kadane’s Algorithm)

### 🔹 Intuition
- A negative running sum will **only reduce** future subarray sums
- If the current sum becomes negative, **reset it to 0**
- Track the maximum sum seen so far

At each index, decide:
- Extend the current subarray
- OR start a new subarray from the current element

---

### 🔹 Core Idea
Maintain two variables:
- `currentSum` → sum of the current subarray
- `maxSum` → maximum sum found so far

---

## ⚠️ Edge Cases

| Case | Handling |
|----|----|
| All elements negative | Maximum element is the answer |
| Single element | That element itself |
| Array contains zero | Works naturally |
| Mixed positive & negative | Optimal subarray is tracked |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`  
  Single traversal of the array.
- **Space Complexity:** `O(1)`  
  No extra space used.

This is **optimal**.

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

long long maxSubarraySum(vector<int>& arr) {
    long long maxSum = LLONG_MIN;
    long long currentSum = 0;

    for (int i = 0; i < arr.size(); i++) {
        currentSum += arr[i];
        maxSum = max(maxSum, currentSum);

        if (currentSum < 0) {
            currentSum = 0;
        }
    }

    return maxSum;
}

Sample Output
Input  : [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output : 6

 **Pattern Learned**

Dynamic Programming (State Optimization)

Used in:

Maximum subarray problems

Stock buy/sell problems

Prefix sum optimizations

Continuous segment problems

✅ Key Takeaway

If the running sum becomes negative, it can never contribute to a maximum subarray — reset it.

Kadane’s Algorithm is a must-know pattern for interviews.
