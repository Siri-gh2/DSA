# 🏆 K-th Smallest and K-th Largest Element in an Array

### 📌 Problem Links
- [GeeksforGeeks – K-th Smallest Element](https://www.geeksforgeeks.org/problems/kth-smallest-element5635/1)
- [Code360 – K-th Smallest and Largest Element of Array](https://www.naukri.com/code360/problems/kth-smallest-and-largest-element-of-array_1115488)

---

## 🧠 Concept

The problem asks us to find:
- the **k-th smallest** element  
- and/or the **k-th largest** element  

from an unsorted array.

Example:
Array = [7, 10, 4, 3, 20, 15]
k = 3

Sorted Array = [3, 4, 7, 10, 15, 20]
k-th smallest = 7
k-th largest = 10


This problem is important because it teaches **selection techniques** and **optimization beyond sorting**.

---

## 📐 Approaches

### 🔹 Approach 1: Sorting (Baseline)

#### Idea
1. Sort the array
2. k-th smallest → `arr[k-1]`
3. k-th largest → `arr[n-k]`

#### When to use
- Simple implementation
- Acceptable for small/medium inputs
- Coding platforms without strict optimization requirements

#### Complexity
- **Time:** `O(n log n)`
- **Space:** `O(1)` (ignoring recursion stack)
- 
---

## 💻 C++ Code – Sorting Approach


```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> kthSmallLarge(vector<int>& arr, int n, int k) {
    sort(arr.begin(), arr.end());

    int kthSmallest = arr[k - 1];
    int kthLargest  = arr[n - k];

    return {kthSmallest, kthLargest};
}

🔹 Approach 2: Heap (Optimised)
🔑 Key Insight

k-th smallest → use a Max Heap of size k

k-th largest → use a Min Heap of size k

We only keep k elements in the heap at any time, avoiding full sorting.

Heap Srategy:
| Target        | Heap Type | Heap Size | Result   |
| ------------- | --------- | --------- | -------- |
| k-th smallest | Max Heap  | k         | Heap top |
| k-th largest  | Min Heap  | k         | Heap top |

💻 C++ Code – Heap (Optimised)
#include <bits/stdc++.h>
using namespace std;

vector<int> kthSmallLarge(vector<int>& arr, int n, int k) {
    priority_queue<int> maxHeap; // for k-th smallest
    priority_queue<int, vector<int>, greater<int>> minHeap; // for k-th largest

    for (int i = 0; i < n; i++) {
        // k-th smallest
        maxHeap.push(arr[i]);
        if (maxHeap.size() > k)
            maxHeap.pop();

        // k-th largest
        minHeap.push(arr[i]);
        if (minHeap.size() > k)
            minHeap.pop();
    }

    return {maxHeap.top(), minHeap.top()};
}


⏱ Complexity Analysis (Heap)

Time Complexity: O(n log k)

Space Complexity: O(k)

This is significantly faster than sorting when k << n.

🟢 Sample Output

Input:

Array = [7, 10, 4, 3, 20, 15]
k = 3


Output:

K-th Smallest = 7
K-th Largest  = 10

🧩 Patterns Learned

Top-K Elements Pattern

Heap-based optimization

Space–time tradeoff

Selection without full sorting

❌ Common Mistakes

Sorting inside loops

Comparing k with array values instead of heap size

Using wrong heap type (min vs max)

Looping over heap size instead of array size

✅ Key Takeaway

When a problem asks for the k-th smallest or largest element, don’t rush to sort — think in terms of heaps and selection.
