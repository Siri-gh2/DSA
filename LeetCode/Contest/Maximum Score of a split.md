# Maximum Score of a Split

**LeetCode Weekly Contest – Medium**

---

## 🧩 Problem Statement

You are given an integer array `nums` of length `n`.

Choose an index `i` such that:

0 ≤ i < n - 1

For a chosen split index `i`:

- `prefixSum(i)` is the sum of elements:
  nums[0] + nums[1] + ... + nums[i]

  
- `suffixMin(i)` is the minimum value among:

nums[i + 1], nums[i + 2], ..., nums[n - 1]


The **score** of a split at index `i` is defined as:

score(i) = prefixSum(i) - suffixMin(i)


Your task is to return the **maximum score** over all valid split indices.

---

## 📥 Input Format

- An integer array `nums` of size `n`

---

## 📤 Output Format

- Return a single integer representing the **maximum score**

---

## 🧪 Examples

### Example 1

Input: nums = [10, -1, 3, -4, -5]
Output: 17


**Explanation:**
- Best split at `i = 2`
- `prefixSum(2) = 10 + (-1) + 3 = 12`
- `suffixMin(2) = min(-4, -5) = -5`
- `score = 12 - (-5) = 17`

---

### Example 2
Input: nums = [-7, -5, 3]
Output: -2

yaml
Copy code

---

## 💡 Approach

A brute-force solution would take **O(n²)** time by recalculating sums and minimums for every split — this is inefficient.

### Optimized Strategy (O(n))

1. Traverse from the right to maintain the **suffix minimum**
2. Traverse from the left while maintaining the **prefix sum**
3. At each valid split:
score = prefixSum - suffixMin

yaml
Copy code
4. Track the maximum score

⚠️ **Important:**  
Prefix sums can overflow `int`, so we must use **`long long`**.

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## ✅ C++ Solution (Using `long long`)

```cpp
class Solution {
public:
 long long maximumScore(vector<int>& nums) {
     int n = nums.size();

     long long suffixMin = nums[n - 1];
     long long prefixSum = 0;
     long long maxScore = LLONG_MIN;

     for (int i = n - 2; i >= 0; i--) {
         prefixSum += nums[i];
         maxScore = max(maxScore, prefixSum - suffixMin);
         suffixMin = min(suffixMin, (long long)nums[i]);
     }

     return maxScore;
 }
};

**📌 Key Takeaways**

Always consider overflow in prefix/sum problems

Use long long when constraints allow large values

Prefix + suffix techniques are common in contest problems
