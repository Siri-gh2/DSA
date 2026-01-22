# Move All Negative Elements in an Array

This problem focuses on rearranging an array so that **negative and positive elements are grouped**, while **preserving their relative order**.

---

## 📌 Problem Links
- [Code360 – Move All Negative Numbers to Beginning and Positive to End](https://www.naukri.com/code360/problems/move-all-negative-numbers-to-beginning-and-positive-to-end_1112620?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker&leftPanelTabValue=SUBMISSION)
- [GeeksforGeeks – Move All Negative Elements to End](https://www.geeksforgeeks.org/problems/move-all-negative-elements-to-end1813/1)

---

## 🧠 Concept

Given an unsorted array containing both **negative and positive integers**, the task is to **rearrange the array** such that:
- All negative elements are grouped together
- All positive (and zero) elements are grouped together
- **The relative order of elements is preserved**

Example:
Input : [1, -2, 3, -4, 5]
Output : [-2, -4, 1, 3, 5]


This is a classic example of a **stable partitioning problem**.

---

## 📐 Approach (Stable Partition Using Extra Space)

### 🔹 Idea
- Since the order must be preserved, **swapping is not allowed**
- Traverse the array and:
  - First collect all **negative elements** in order
  - Then collect all **positive and zero elements** in order
- Combine both to form the final array

---

### 🔹 Why this works
- Traversing left to right naturally preserves order
- No element is rearranged out of sequence
- Simple and reliable for all edge cases

---

## ⚠️ Edge Cases

| Case | Result |
|----|----|
| All elements negative | Array remains unchanged |
| All elements positive | Array remains unchanged |
| Single element | No change |
| Empty array | No operation |
| Presence of `0` | Treated as positive |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`  
  Two linear traversals of the array.
- **Space Complexity:** `O(n)`  
  Extra array used to preserve order.

This tradeoff is **intentional and expected** for stable rearrangement.

---

## 💻 C++ Implementation ( negatives at begining)  

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> separateNegativeAndPositive(vector<int> &arr){
    int n = arr.size();
    vector<int> result;
    result.reserve(n);

    // store negative elements first
    for(int i = 0; i < n; i++) {
        if(arr[i] < 0) {
            result.push_back(arr[i]);
        }
    }

    // store positive and zero elements
    for(int i = 0; i < n; i++) {
        if(arr[i] >= 0) {
            result.push_back(arr[i]);
        }
    }

    return result;
}

---

## 💻 C++ Implementation ( negatives at end)

```cpp

class Solution {
  public:
    void segregateElements(vector<int>& arr) {
        // Your code goes here
        int n = arr.size();
        vector<int> p;
        
        for(int i =0;i<n;i++)
        {
            if(arr[i]>=0)
            {
                p.push_back(arr[i]);
            }
        }
        for(int i =0;i<n;i++)
        {
            if(arr[i]<0)
            {
                p.push_back(arr[i]);
            }
        }
        for(int i =0;i<n;i++)
        {
            arr[i] = p[i];
        }
        
    }
};

**Pattern Learned**

Stable Partitioning

Used in:

Segregating elements with order constraints

Filtering problems

Data preprocessing

Variants of array rearrangement

✅ Key Takeaway

When relative order matters, prefer stable approaches using extra space over clever in-place tricks.
