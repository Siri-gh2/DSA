#  Non-overlapping Intervals

🔗 **Problem Link:**  
https://leetcode.com/problems/non-overlapping-intervals/

---

##  Problem Explanation

You are given an array of intervals where each interval is represented as  
`[start, end]`.

An interval **overlaps** with another if they share any common time.

Your task is to **remove the minimum number of intervals** so that the remaining intervals **do not overlap**.

---

##  Key Insight

Instead of deciding **which intervals to remove**, it is easier to decide  
**which intervals to keep**.

If we maximize the number of **non-overlapping intervals**, then:

intervals to remove = total intervals − non-overlapping intervals


---

## 🧠 Approach (Greedy)

1. **Sort intervals by their ending time**  
   - This ensures we always pick the interval that finishes earliest, leaving more room for others.

2. **Select intervals greedily**
   - Always pick the first interval.
   - For every next interval:
     - If its start time is **greater than or equal to** the end time of the last selected interval → keep it.
     - Otherwise → it overlaps, so skip it.

3. **Final Answer**
   - `total intervals - selected intervals`

This is the same greedy idea used in **Activity Selection** problems.

---

##  Base Cases

- If the input array is empty → return `0`
- If there is only one interval → no removal needed

---

##  Complexity Analysis

- **Time Complexity:** `O(n log n)`  
  (due to sorting)

- **Space Complexity:** `O(1)`  
  (sorting in-place, no extra data structures)

---

## 💻 C++ Code

```cpp
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        int n = intervals.size();
        if (n == 0) return 0;

        sort(intervals.begin(), intervals.end(), [](auto &a, auto &b) {
            return a[1] < b[1];
        });

        int count = 1;
        int lastEnd = intervals[0][1];

        for (int i = 1; i < n; i++) {
            if (intervals[i][0] >= lastEnd) {
                count++;
                lastEnd = intervals[i][1];
            }
        }

        return n - count;
    }
};
```

**Why This Works**

Sorting by end time guarantees minimum overlap

Greedy choice is always optimal here

This solution is accepted, optimal, and interview-safe

** Summary**

Classic greedy problem

Think in terms of keeping max valid intervals

Remove the rest
