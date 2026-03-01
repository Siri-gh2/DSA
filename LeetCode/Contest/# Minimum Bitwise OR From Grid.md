# Minimum Bitwise OR From Grid

## 📌 Problem Overview
Given a 2D integer array `grid` of size $m \times n$, you must select **exactly one** integer from each row. The goal is to minimize the bitwise OR of these selected integers.

### Constraints
* $1 \le m \le 10^5$
* $1 \le n \le 10^5$
* $m \times n \le 10^5$ (Total elements are limited)
* $1 \le \text{grid}[i][j] \le 10^5$ (Values fit in 17 bits)

---

## 💡 Solution Strategy: Greedy Bitmasking

To achieve the **minimum** bitwise OR, we prioritize keeping the most significant bits (MSB) as $0$. 

### The Logic
1. **Iterative Refinement:** We iterate through bits from $16$ down to $0$.
2. **Hypothesis:** For each bit, we check: "Can we satisfy the condition for all rows *without* using this bit?"
3. **Target Mask:** We construct a `target_mask` consisting of:
   * Bits we have already been forced to set to $1$.
   * All bits smaller than the current bit (assuming they could potentially be $0$ or $1$).
4. **Validation:** A row is satisfied if it contains at least one number `num` such that `(num | target_mask) == target_mask`. This condition ensures `num` doesn't have any bits set that aren't allowed by our current budget.

---

## 💻 Implementation (C++)

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    int minimumOR(vector<vector<int>>& grid) {
        int m = grid.size();
        
        // Optimization: Remove duplicate values in each row to reduce iterations
        for (auto& row : grid) {
            sort(row.begin(), row.end());
            row.erase(unique(row.begin(), row.end()), row.end());
        }

        int current_mask = 0;
        
        // Check bits from 16 down to 0
        for (int bit = 16; bit >= 0; --bit) {
            // Test if we can achieve a valid OR without this bit
            // target_mask = (bits already forced) | (all bits below the current bit)
            int target_mask = current_mask | ((1 << bit) - 1);
            
            if (!canAchieve(grid, target_mask)) {
                // If the bit is necessary to satisfy all rows, add it to current_mask
                current_mask |= (1 << bit);
            }
        }

        return current_mask;
    }

private:
    bool canAchieve(const vector<vector<int>>& grid, int mask) {
        for (const auto& row : grid) {
            bool found = false;
            for (int num : row) {
                // Check if num is a submask of the allowed bits
                if ((num | mask) == mask) {
                    found = true;
                    break;
                }
            }
            if (!found) return false;
        }
        return true;
    }
};
```
## Complexity Analysis

Type,Complexity,Explanation
Time,O(17⋅∑elements),We iterate 17 times over the total elements in the grid.
Space,O(1),No extra data structures are used (excluding grid modification).

## Example Walkthrough
- Input:
  ```
  grid = [[3, 5], [6, 4]]
```
Bit 2 (Value 4): - Try target_mask = 3 (binary 011).

Row 0 has 3 (011 | 011 == 011 ✅).

Row 1 has no submask of 011 ❌.

**Result**: Bit 2 is forced ON. current_mask = 4.

- Bit 1 (Value 2): - Try target_mask = 4 | 1 = 5 (binary 101).

Row 0 has 5 (101 | 101 == 101 ✅).

Row 1 has 4 (100 | 101 == 101 ✅).

**Result**: Bit 1 remains OFF.

- Bit 0 (Value 1): - Try target_mask = 4 (binary 100).

Row 0 has no submask of 100 ❌.

**Result**: Bit 0 is forced ON. current_mask = 5.

**Final Answer: 5**
