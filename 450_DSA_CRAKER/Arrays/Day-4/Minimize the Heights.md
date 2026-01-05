# Minimize the Heights (Minimize the Difference)

This problem focuses on minimizing the **difference between the maximum and minimum elements** of an array after modifying each element **exactly once** by either increasing or decreasing it by `k`.

This is a classic **greedy + sorting** problem and is frequently asked in interviews.

---

## 📌 Problem Links
- [Code360 – Minimize the Difference](https://www.codingninjas.com/codestudio/problems/minimize-the-difference_3208652?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker)
- [GeeksforGeeks – Minimize the Heights](https://practice.geeksforgeeks.org/problems/minimize-the-heights3351/1)

---

## 🧠 Concept

You are given an array of **positive integers** and a value `k`.  
You must **either increase or decrease each element by `k` exactly once**, such that:

- All resulting values remain **non-negative**
- The difference between the **maximum and minimum** elements is **minimized**

---

### 🔹 Example
Input : arr = [1, 5, 8, 10], k = 2
Output : 5

Explanation:
After modification → [3, 3, 6, 8]
Max - Min = 8 - 3 = 5


---

## 📐 Approach (Greedy + Sorting)

### 🔹 Key Observations
- Sorting helps compare adjacent elements meaningfully
- Smaller elements are generally **increased by `k`**
- Larger elements are generally **decreased by `k`**
- We try every valid split point to minimize the range

---

### 🔹 Strategy
1. Sort the array
2. Initialize the answer as:
   arr[n-1]-arr[0]

   3. Assume:
- Smallest value = `arr[0] + k`
- Largest value  = `arr[n-1] - k`
4. For each index `i`, try:
- Increasing elements `0..i` by `k`
- Decreasing elements `i+1..n-1` by `k`
5. Ignore any split that causes a **negative height**
6. Update the minimum difference

---

## ⚠️ Edge Cases

| Case | Handling |
|----|----|
| `n <= 1` | Difference is `0` |
| `k = 0` | No change |
| Negative height after decrease | Skip that case |
| Large `k` values | Handled safely |

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n log n)` (due to sorting)
- **Space Complexity:** `O(1)` (no extra space)

This is optimal for this problem.

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

int getMinDiff(vector<int> &arr, int k) {
 int n = arr.size();
 if (n <= 1) return 0;

 sort(arr.begin(), arr.end());

 int ans = arr[n - 1] - arr[0];

 int smallest = arr[0] + k;
 int largest  = arr[n - 1] - k;

 for (int i = 0; i < n - 1; i++) {

     // Skip if height becomes negative
     if (arr[i + 1] - k < 0)
         continue;

     int mini = min(smallest, arr[i + 1] - k);
     int maxi = max(largest,  arr[i] + k);

     ans = min(ans, maxi - mini);
 }

 return ans;
}

Sample Output
Input  : [1, 2, 3, 4, 5], k = 2
Output : 3

🧩 Pattern Learned

Greedy Range Optimization

Used in:

Height adjustment problems

Range minimization

Scheduling & balancing problems

Cost optimization scenarios

✅ Key Takeaway

When each element has a limited modification range, sorting + greedy boundary adjustment is often the optimal approach.
