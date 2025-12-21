# DSA Journey – Arrays (Concepts & Patterns)

This post documents the **array problems** I practiced, focusing on **patterns, optimizations, and interview-ready thinking**. Each problem includes the idea, pitfalls, and complexity — not just code.

---

## Reverse of an Array

**Pattern:** Two Pointers (Partial Reversal)

**Idea:**

* Keep indices `0..m` unchanged
* Reverse subarray from `m+1` to `n-1` using two pointers

**Edge Cases:**

* `m >= n-1` → no change
* `m == -1` → reverse entire array
* `n <= 1` → no change



### 📌 Problem Links
- [Code360 – Reverse the Array](https://www.naukri.com/code360/problems/reverse-the-array_1262298)
- [GeeksforGeeks – Reverse an Array](https://www.geeksforgeeks.org/problems/reverse-an-array/1)

---

## 🧠 Concept

Reversing an array means rearranging its elements so that the first element becomes the last, the second becomes the second last, and so on.

Example:
Input : [1, 2, 3, 4, 5]
Output : [5, 4, 3, 2, 1]

---

## 📐 Approach (Two Pointers)

### 🔹 Idea
- Use two pointers:
  - `left` → start of the array
  - `right` → end of the array
- Swap elements at `left` and `right`
- Move `left` forward and `right` backward
- Stop when `left >= right`

### 🔹 Why this works
Each swap places elements in their correct reversed position.  
Only `n/2` swaps are required, making the solution efficient.

---

## ⚠️ Edge Cases

|      Case            |       Result    |
|----------------------|-----------------|
| Empty array `[]`     | No change       |
| Single element `[x]` | Same array      |
| Two elements `[a, b]'| `[b, a]`        |
| Duplicate values     | Works normally  |


---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> reverseArray(vector<int> &arr) {
    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        swap(arr[left], arr[right]);
        left++;
        right--;
    }

    return arr;
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    vector<int> result = reverseArray(arr);

    for (int x : result) {
        cout << x << " ";
    }
    return 0;
}

Sample Output:
5 4 3 2 1

🧩** Pattern Learned**

Two Pointer Technique

Used in:

Array reversal

String reversal

Rotate array

Palindrome checking

Partitioning problems


