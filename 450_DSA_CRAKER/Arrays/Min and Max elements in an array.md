# Find Minimum & Maximum Element in an Array  
(and Sum of Minimum & Maximum)

This problem focuses on finding the **smallest** and **largest** elements in an array efficiently using a single traversal.

---

## 🧠 Concept

Given an array of integers, the task is to determine:
- the **minimum element**
- the **maximum element**
- and optionally, the **sum of both**

Example:

Input : [3, 5, 1, 8, 2]
Minimum: 1
Maximum: 8
Sum : 9


This is a **fundamental array problem** frequently asked in interviews to test:
- loop control
- edge case handling
- optimization thinking (avoiding repeated scans)

---

## 📐 Approach (Single Traversal)

### 🔹 Idea
- Initialize both `min` and `max` with the **first element**
- Traverse the array once
- Update `min` when a smaller element is found
- Update `max` when a larger element is found

This avoids scanning the array multiple times and gives the **optimal solution**.

### 🔹 Why this works
Every element is compared exactly once, so we get both values in **one pass**.

---

## ⚠️ Edge Cases

| Case | Result |
|----|----|
| Empty array | Handle separately |
| Single element | Min = Max = that element |
| All elements same | Min and Max remain same |
| All negative values | Works normally |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`  
  Only one traversal of the array.
- **Space Complexity:** `O(1)`  
  No extra space used.

---

## 💻 C++ Implementation – Find Min & Max

```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> getMinMax(vector<int>& arr) {
    int n = arr.size();

    if (n == 0)
        return {-1, -1};   // depends on constraints

    int mini = arr[0];
    int maxi = arr[0];

    for (int i = 1; i < n; i++) {
        if (arr[i] < mini)
            mini = arr[i];
        if (arr[i] > maxi)
            maxi = arr[i];
    }

    return {mini, maxi};
}

C++ Implementation – Sum of Min & Max

#include <bits/stdc++.h>
using namespace std;

int sumOfMaxMin(int arr[], int n) {
    if (n == 0)
        return 0;

    int mini = arr[0];
    int maxi = arr[0];

    for (int i = 1; i < n; i++) {
        if (arr[i] < mini)
            mini = arr[i];
        if (arr[i] > maxi)
            maxi = arr[i];
    }

    return mini + maxi;
}

🟢 Sample Output
Input : [3, 5, 1, 8, 2]
Output:
Minimum = 1
Maximum = 8
Sum     = 9

Pattern Learned

Single-Pass Optimization

Used in:

Min / Max problems

Range calculations

Kadane’s Algorithm

Prefix-based logic

✅ Key Takeaway

If a problem asks for multiple values from an array, try to compute them together in one traversal instead of scanning repeatedly.



