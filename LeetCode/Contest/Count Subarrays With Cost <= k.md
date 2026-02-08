# Count Subarrays With Cost ≤ K

🔗 **Problem Link**:  
https://leetcode.com/contest/weekly-contest-488/problems/count-subarrays-with-cost-less-than-or-equal-to-k/

---

##  Problem Statement
You are given an integer array `arr` and an integer `k`.

For any subarray `arr[l..r]`, define the **cost** as:

```
cost = (max(arr[l..r]) - min(arr[l..r])) * (r - l + 1)
```

Return the number of subarrays whose cost is **less than or equal to `k`**.

A subarray is a contiguous non-empty sequence of elements.

---

## 💡 Example

Input: arr = [1,3,2], k = 4
Output: 5


Valid subarrays:
```
[1] -> 0
[1,3] -> 4
[3] -> 0
[3,2] -> 2
[2] -> 0

```

---

## 🚨 Observations
If we try all subarrays and compute max & min every time:

- Number of subarrays → **O(n²)**
- Finding max/min → **O(n)**

Total → **O(n³)** ❌ (TLE for large inputs)

Even improving max/min with preprocessing still leads to **O(n²)** → risky.

We need near **O(n)**.

---

## 🧠 Key Concept

Whenever a problem has:

- contiguous segment  
- expanding / shrinking range  
- condition must stay valid  

👉 think **Sliding Window**.

But we also need fast:
- maximum in window  
- minimum in window  

👉 use **Monotonic Deques**.

They allow us to maintain max/min in **O(1)** amortized time.

---

## 🎯 Approach

We maintain:
```
- `l` → left boundary of window  
- `r` → right boundary (current index)
```
For each step:

1. Insert `arr[r]` into:
   - decreasing deque → gives maximum
   - increasing deque → gives minimum

2. If
 ```
   (max - min) * window_size > k
 ```  
move `l` forward until valid.

4. Every valid window contributes:
    r-l +1

subarrays ending at `r`.

---

## 🔥 Why `r - l + 1`?

Because once `[l..r]` is valid, then:
```
[l..r], [l+1..r], [l+2..r] ... [r..r]
```

are all valid.

---

## 🧭 Hints (Contest Mindset)

If you see:

✅ subarrays  
✅ max/min  
✅ large constraints  

→ almost always **monotonic deque + sliding window**.

Train your brain to detect this fast.

---

## ⏱ Complexity
Each index enters and leaves deque once.
```
Time : O(n)
Space : O(n)
```

---

## 💻 C++ Code

```cpp
class Solution {
public:
    long long countSubarrays(vector<int>& arr, long long k) {
        int n = arr.size();
        
        deque<int> maxdq, mindq;
        long long ans = 0;
        int l = 0;
        
        for (int r = 0; r < n; r++) {
            
            while (!maxdq.empty() && arr[maxdq.back()] <= arr[r])
                maxdq.pop_back();
            maxdq.push_back(r);
            
            while (!mindq.empty() && arr[mindq.back()] >= arr[r])
                mindq.pop_back();
            mindq.push_back(r);
            
            while (!maxdq.empty() && !mindq.empty() &&
                   (long long)(arr[maxdq.front()] - arr[mindq.front()]) * (r - l + 1) > k) {
                
                if (maxdq.front() == l) maxdq.pop_front();
                if (mindq.front() == l) mindq.pop_front();
                l++;
            }
            
            ans += (r - l + 1);
        }
        
        return ans;
    }
};

```
### Takeaway

This is a classic pattern-compression problem.

Master monotonic deque once → you unlock many hard sliding window questions.

```
Sliding window + dynamic max/min = powerful weapon.
```

