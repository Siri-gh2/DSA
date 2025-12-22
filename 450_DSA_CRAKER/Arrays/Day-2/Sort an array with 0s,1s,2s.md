# Sort an Array of 0s, 1s, and 2s

This problem focuses on sorting an array containing only `0`, `1`, and `2` **without using any sorting algorithm**, in linear time and constant space.

---

## 🧠 Concept

Given an array consisting only of `0`, `1`, and `2`, the task is to sort the array in ascending order.

Example:
Input : [0, 2, 1, 2, 0, 1]
Output : [0, 0, 1, 1, 2, 2]


This problem is a classic application of the **Dutch National Flag Algorithm**, which is commonly asked in interviews to test:
- pointer manipulation
- in-place sorting
- loop control and invariants

---

## 📐 Approach (Dutch National Flag Algorithm)

### 🔹 Idea

Use **three pointers** to partition the array into regions:

- `l` → boundary for `0`s
- `i` → current index
- `r` → boundary for `2`s

The array is divided as:

[0 ... l-1] → all 0s
[l ... i-1] → all 1s
[i ... r] → unknown
[r+1 ... n-1] → all 2s


---

### 🔹 Core Logic

- If `arr[i] == 0`
  - swap with `arr[l]`
  - increment both `l` and `i`
- If `arr[i] == 1`
  - just increment `i`
- If `arr[i] == 2`
  - swap with `arr[r]`
  - decrement `r`
  - **do not increment `i`** (new value must be checked)

---

### 🔹 Why this works

- Every swap places an element into its correct partition
- The unknown region shrinks continuously
- Each element is processed **at most once**

---

## ⚠️ Edge Cases

| Case | Result |
|----|----|
| Empty array | No change |
| All elements same | Already sorted |
| Already sorted array | One pass only |
| Reverse order | Still sorted in one traversal |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`  
  Each element is visited once.
- **Space Complexity:** `O(1)`  
  In-place sorting without extra memory.

---

## 💻 C++ Implementation

```cpp
class Solution {
  public:
    void sort012(vector<int>& arr) {
        int n = arr.size();
        int l = 0, i = 0, r = n - 1;

        while (i <= r) {
            if (arr[i] == 0) {
                swap(arr[i], arr[l]);
                l++;
                i++;
            }
            else if (arr[i] == 1) {
                i++;
            }
            else { // arr[i] == 2
                swap(arr[i], arr[r]);
                r--;
            }
        }
    }
};


Sample Output
Input  : [0, 2, 1, 2, 0, 1]
Output : [0, 0, 1, 1, 2, 2]

Pattern Learned

Dutch National Flag Algorithm

Used in:

Partitioning problems

Three-way sorting

Array segregation

Quicksort-style logic

Key Takeaway

When array values are limited to a small known set, partitioning with pointers can achieve optimal O(n) time without extra space.
