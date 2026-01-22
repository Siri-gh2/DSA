# Rotate an Array (Left Rotation & Cyclic Rotation)

This problem focuses on **rotating an array** by a given number of steps.  
It is a very common interview problem and helps build clarity on **index manipulation and in-place algorithms**.

---

## 📌 Problem Links
- [Code360 – Rotate Array (Left Rotation by k)](https://www.naukri.com/code360/problems/rotate-array_1230543?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker)
- [GeeksforGeeks – Cyclically Rotate an Array by One](https://www.geeksforgeeks.org/problems/cyclically-rotate-an-array-by-one2614/1)

---

## 🧠 Concept

Array rotation means shifting elements of an array in a circular manner.

There are two common variants:
1. **Left Rotation by `k`**
2. **Right (Cyclic) Rotation by `1` or `k`**

---

### 🔹 Left Rotation by `k`
Each element moves `k` positions to the **left**.

Example:
Input : [1, 2, 3, 4, 5], k = 2
Output : [3, 4, 5, 1, 2]


---

### 🔹 Right (Cyclic) Rotation by `1`
The last element comes to the front.

Example:

Input : [1, 2, 3, 4, 5]
Output : [5, 1, 2, 3, 4]


---

## 📐 Approach 1: Reversal Algorithm (Optimal)

The **reversal algorithm** allows rotating the array:
- in `O(n)` time
- using `O(1)` extra space

---

## ✅ Left Rotation by `k` (Reversal Method)

### 🔹 Steps
1. Reverse the first `k` elements
2. Reverse the remaining `n - k` elements
3. Reverse the entire array

---

### 💻 C++ Code (Left Rotation)

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> rotateArray(vector<int> arr, int k) {
    int n = arr.size();
    if (n <= 1) return arr;

    k = k % n;
    if (k == 0) return arr;

    // reverse first k elements
    reverse(arr.begin(), arr.begin() + k);

    // reverse remaining elements
    reverse(arr.begin() + k, arr.end());

    // reverse entire array
    reverse(arr.begin(), arr.end());

    return arr;
}

✅ Cyclic Rotation by One (Right Rotation)
🔹 Idea

Store the last element

Shift all elements one step to the right

Place the stored element at index 0

**C++ Code (Right Rotation by 1)**

class Solution {
  public:
    void rotate(vector<int> &arr) {
        int n = arr.size();
        if (n <= 1) return;

        int last = arr[n - 1];

        for (int i = n - 1; i > 0; i--) {
            arr[i] = arr[i - 1];
        }

        arr[0] = last;
    }
};
**EDGE CASES:**
| Case         | Result            |
| ------------ | ----------------- |
| `k = 0`      | No rotation       |
| `k > n`      | Use `k = k % n`   |
| `n = 0 or 1` | No change         |
| Large `k`    | Handled by modulo |

⏱ Complexity Analysis
Reversal Algorithm

Time Complexity: O(n)

Space Complexity: O(1)

Cyclic Rotation by One

Time Complexity: O(n)

Space Complexity: O(1)

🧩 Pattern Learned

Array Reversal + Modulo Optimization

Used in:

Array rotation problems

String rotations

Circular shifts

Deque-based problems

✅ Key Takeaway

Always clarify the direction of rotation before coding.
The reversal algorithm is the most efficient and interview-preferred solution.

