# Job Sequencing Problem (Greedy Scheduling)

This problem asks you to schedule jobs to **maximize total profit** given that:
- Each job takes **1 unit of time**
- Each job has a **deadline** and a **profit**
- Only one job can be performed at a time

We will look at two variations of this problem and provide **both standard and optimized (DSU)** solutions.

---

## 📌 Problem Links

- [GeeksforGeeks – Job Sequencing Problem](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)
- [Code360 – Job Sequencing Problem](https://www.naukri.com/code360/problems/job-sequencing-problem_1169460?topList=love-babbar-dsa-sheet-problems&utm_source=website&utm_medium=affiliate&utm_campaign=450dsatracker&leftPanelTabValue=PROBLEM)

---

## 🧠 Concept

You are given a list of jobs, each with:
- a **deadline**
- a **profit**

Goal:  
Schedule jobs such that the total profit is **maximized** and all jobs complete within their deadlines.

---

# 🎯 Key Insight (Greedy)

1. High-profit jobs should be prioritized.
2. Each job should be placed at the **latest available time slot** before its deadline.
3. By doing this, we **maximize profit** while respecting deadlines.

---

## 📊 Input Formats

### 🔹 GfG Format

Each job is given as:
JobID Deadline Profit

Example:


1 2 30
2 2 40
3 1 10
4 1 10


### 🔹 Code360 Format

Each job is given as:
[deadline, profit]

Example:


[2, 30], [2, 40], [1, 10], [1, 10]


In both cases the logic is the same — only the parsing code differs.

---

## 📐 Standard Greedy Solution

### 🔹 Approach

1. Pair job attributes (deadline, profit).
2. Sort jobs by **profit descending**.
3. Use an array for slots of size **max deadline + 1**.
4. For each job, try to schedule it in the **latest free slot ≤ deadline**.
5. Count scheduled jobs and sum profits.

---

## 💻 C++ Implementation — Standard (GfG)

```cpp
vector<int> jobScheduling(vector<vector<int>> &jobs)
{
    int n = jobs.size();

    // Sort by profit (index 2)
    sort(jobs.begin(), jobs.end(), [](auto &a, auto &b) {
        return a[2] > b[2];
    });

    int maxDeadline = 0;
    for (auto &job : jobs)
        maxDeadline = max(maxDeadline, job[1]);

    vector<bool> slot(maxDeadline + 1, false);
    int jobCount = 0, totalProfit = 0;

    for (auto &job : jobs) {
        int deadline = job[1], profit = job[2];
        for (int t = deadline; t > 0; t--) {
            if (!slot[t]) {
                slot[t] = true;
                jobCount++;
                totalProfit += profit;
                break;
            }
        }
    }

    return {jobCount, totalProfit};
}

```
## 💻 C++ Implementation — Standard (Code360)

vector<int> jobScheduling(vector<vector<int>> &jobs)
{
    int n = jobs.size();

    // Sort by profit (second element)
    sort(jobs.begin(), jobs.end(), [](auto &a, auto &b) {
        return a[1] > b[1];
    });

    int maxDeadline = 0;
    for (auto &job : jobs)
        maxDeadline = max(maxDeadline, job[0]);

    vector<bool> slot(maxDeadline + 1, false);
    int jobCount = 0, totalProfit = 0;

    for (auto &job : jobs) {
        int deadline = job[0], profit = job[1];
        for (int t = deadline; t > 0; t--) {
            if (!slot[t]) {
                slot[t] = true;
                jobCount++;
                totalProfit += profit;
                break;
            }
        }
    }

    return {jobCount, totalProfit};
}
```

🚀 Optimized Version (DSU)

When maxDeadline is large, the inner loop can be slow.
We can use Disjoint Set Union to find the nearest free slot efficiently.

## 💻 C++ Implementation — Optimized (DSU)

class Solution {
  public:
    int find(int x, vector<int>& parent) {
        if (parent[x] == x)
            return x;
        return parent[x] = find(parent[x], parent);
    }

    vector<int> jobScheduling(vector<vector<int>>& jobs) {
        int n = jobs.size();

        sort(jobs.begin(), jobs.end(), [](auto &a, auto &b) {
            return a[1] > b[1];
        });

        int maxDeadline = 0;
        for (auto &job : jobs)
            maxDeadline = max(maxDeadline, job[0]);

        vector<int> parent(maxDeadline + 1);
        for (int i = 0; i <= maxDeadline; i++)
            parent[i] = i;

        int jobCount = 0, totalProfit = 0;

        for (auto &job : jobs) {
            int available = find(job[0], parent);

            if (available > 0) {
                parent[available] = find(available - 1, parent);
                jobCount++;
                totalProfit += job[1];
            }
        }

        return {jobCount, totalProfit};
    }
};

```

Complexity Summary


|       Version |                Time Complexity | Space Complexity |
| ------------: | -----------------------------: | ---------------: |
|      Standard | `O(n log n + n × maxDeadline)` | `O(maxDeadline)` |
| DSU Optimized |                   `O(n log n)` | `O(maxDeadline)` |

Example

Input:

4
1 2 30
2 2 40
3 1 10
4 1 10


Output:

2 70

 Patterns Learned:

Greedy scheduling

Sorting by custom criteria

Slot management

Union-Find for optimization

 Common Mistakes: 

Sorting by deadline instead of profit

Forgetting to match profit with its deadline

Ignoring 1-based slot indexing

Using incorrect loop direction

✅ Key Takeaway

To maximize profit with deadlines, always greedily choose higher-profit jobs and schedule them as late as possible.

