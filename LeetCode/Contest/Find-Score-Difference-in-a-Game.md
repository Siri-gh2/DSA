# Find Score Difference in a Game

## 🧩 Problem Summary

You are given an integer array `nums`, where `nums[i]` represents the points scored in the `i-th` game.

There are exactly two players:
- Player 1 starts as active.
- Player 2 starts as inactive.

For each game (processed left to right):

1. If `nums[i]` is odd → swap active and inactive players.
2. If it is every 6th game (index 5, 11, 17, ...) → swap roles.
3. The active player gains `nums[i]` points.

Return the **score difference**:
Player1_total - Player2_total

---

## 💡 Approach

- Track:
  - `score1`
  - `score2`
  - `active` (0 → Player1, 1 → Player2)
- For each index:
  - If odd → toggle active
  - If `(i % 6 == 5)` → toggle active
  - Add points to active player
- Return `score1 - score2`

---

## ⏱ Complexity

- Time: `O(n)`
- Space: `O(1)`

---

## 💻 C++ Code

```cpp
class Solution {
public:
    int scoreDifference(vector<int>& nums) {
        int score1 = 0, score2 = 0;
        int active = 0;  // 0 -> Player 1, 1 -> Player 2
        
        for (int i = 0; i < nums.size(); i++) {
            
            if (nums[i] % 2 == 1) {
                active ^= 1;
            }
            
            if (i % 6 == 5) {
                active ^= 1;
            }
            
            if (active == 0)
                score1 += nums[i];
            else
                score2 += nums[i];
        }
        
        return score1 - score2;
    }
};

```
## 🧠 What I Understood

- There are only two players, and only one is active at a time.
- The order of operations matters:
  1. If the current value is odd → swap players.
  2. If it is every 6th game → swap players.
  3. Then the active player gets the points.
- Swapping can happen twice in the same index.
- We don’t simulate players separately — we just track who is active using a toggle.
- Final answer is simply:
  Player1_total - Player2_total
- This is a pure simulation problem — no math trick, just careful implementation.
