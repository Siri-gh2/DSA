# Activity Selection Problem (Greedy)

##  Topic
Greedy Algorithm

---

##  Concept

The **Activity Selection Problem** is a classic greedy problem where we aim to select the **maximum number of non-overlapping activities** from a given set.

Each activity has:
- a **start time**
- a **finish time**

Only **one activity can be performed at a time**.

The greedy insight is simple but powerful:
> Always pick the activity that **finishes first**, leaving maximum room for the remaining activities.

---

## ❓ Problem Statement

You are given two arrays:
- `start[]` → start times of activities  
- `finish[]` → finish times of activities  

Your task is to return the **maximum number of activities** that can be performed by a single person such that no activities overlap.

### Problem Links
- 🔗 GeeksforGeeks:  
  https://www.geeksforgeeks.org/problems/activity-selection-1587115620/1  
- 🔗 Coding Ninjas / Code360:  
  https://www.naukri.com/code360/problems/maximum-activities_1062712  

---

## 💡 Approach (Greedy Strategy)

1. **Pair** each activity as `(start, finish)`
2. **Sort activities by finish time**
3. **Select the first activity** (earliest finish)
4. For every next activity:
   - Select it **only if**  
     `start_time >= last_selected_finish_time`

Why this works:
- Finishing earlier frees time for more activities
- Greedy choice at each step leads to the optimal solution

---

## 🧪 Base Cases

- If there are **no activities (`n == 0`)**, return `0`
- After sorting, the **first activity is always selected**

---

## 🧾 C++ Solution (With Comments)

```cpp
#include <algorithm>
#include <vector>
using namespace std;

int maximumActivities(vector<int> &start, vector<int> &finish) {
    int n = start.size();
    
    // Base case: no activities
    if (n == 0) return 0;

    // Step 1: Store activities as (start, finish) pairs
    vector<pair<int, int>> activities(n);
    for (int i = 0; i < n; i++) {
        activities[i] = {start[i], finish[i]};
    }

    // Step 2: Sort activities by finish time
    sort(activities.begin(), activities.end(),
         [](pair<int, int>& a, pair<int, int>& b) {
             return a.second < b.second;
         });

    // Step 3: Select the first activity
    int count = 1;
    int lastEnd = activities[0].second;

    // Step 4: Select remaining compatible activities
    for (int i = 1; i < n; i++) {
        if (activities[i].first >= lastEnd) {
            count++;
            lastEnd = activities[i].second;
        }
    }

    return count;
}


**Time & Space Complexity**

Time Complexity:
O(n log n) → due to sorting

Space Complexity:
O(n) → for storing activity pairs

📝 Key Takeaways

Sorting by finish time is the core greedy insight

Use >= (not >) to allow back-to-back activities

Simple logic, but very common in interviews

✅ Status

✔️ Interview-ready
✔️ Accepted on GFG & Code360
✔️ Part of Love Babbar DSA Sheet
