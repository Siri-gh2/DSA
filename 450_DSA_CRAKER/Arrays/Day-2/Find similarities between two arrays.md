# Find Similarities Between Two Arrays

This problem focuses on finding the **similarity** between two arrays in terms of:
- the number of **common elements** (intersection)
- the total number of **distinct elements** (union)

---

## 📌 Problem Links
- [Code360 – Find Similarities Between Two Arrays](https://www.naukri.com/code360/problems/find-similarities-between-two-arrays_1229070?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker&leftPanelTabValue=PROBLEM)
- [GeeksforGeeks – Union of Two Arrays](https://www.geeksforgeeks.org/problems/union-of-two-arrays3538/1)

---

## 🧠 Concept

Given two arrays, the task is to determine:
1. **Intersection count** → number of elements present in **both** arrays
2. **Union count** → number of **distinct** elements present in **either** array

Example:
arr1 = [1, 2, 3]
arr2 = [2, 3, 4]

Intersection count = 2 (2, 3)
Union count = 4 (1, 2, 3, 4)



This problem is commonly used to test understanding of:
- sets and uniqueness
- union vs intersection
- clean handling of duplicates

---

## 📐 Approach (Using Set)

### 🔹 Idea
- Use a `set` to store unique elements
- Insert all elements of the first array into the set
- Traverse the second array:
  - If an element already exists in the set → it contributes to **intersection**
  - Insert the element into the set (set ensures uniqueness)
- At the end:
  - **Intersection count** is the number of common elements
  - **Union count** is the size of the set

---

### 🔹 Why this works
- A set automatically removes duplicates
- Lookup in a set helps identify common elements
- Sorted order is maintained naturally (useful for union problems)

---

## ⚠️ Edge Cases

| Case | Result |
|----|----|
| One array empty | Intersection = 0, Union = size of other array |
| Both arrays empty | Intersection = 0, Union = 0 |
| All elements same | Intersection = size of unique elements |
| Negative values | Handled normally |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O((n + m) log(n + m))`  
  Each insertion/search in a set takes `log` time.
- **Space Complexity:** `O(n + m)`  
  Extra space for storing unique elements.

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> findSimilarity(vector<int> arr1, vector<int> arr2, int n, int m) {
    set<int> s;
    int intersection = 0;

    // insert elements of first array
    for (int i = 0; i < n; i++) {
        s.insert(arr1[i]);
    }

    // process second array
    for (int i = 0; i < m; i++) {
        if (s.find(arr2[i]) != s.end()) {
            intersection++;
        }
        s.insert(arr2[i]);
    }

    int unionCount = s.size();

    return {intersection, unionCount};
}
🟢 Sample Output

Input:
arr1 = [1, 2, 3]
arr2 = [2, 3, 4]

Output:
Intersection = 2
Union        = 4

Pattern Learned

Set-Based Deduplication

Used in:

Union & Intersection problems

Removing duplicates

Similarity checks

Data preprocessing tasks

✅ Key Takeaway

Sets are ideal when you need uniqueness + efficient lookup for union and intersection style problems.
