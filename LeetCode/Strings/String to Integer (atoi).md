# String to Integer (atoi)

## 🔗 Problem Link
- LeetCode: https://leetcode.com/problems/string-to-integer-atoi/

---

## 🧠 Problem Statement

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer.

The algorithm should:
1. Ignore leading whitespaces.
2. Determine the sign (`+` or `-`).
3. Read digits until a non-digit character is encountered.
4. Clamp the result within the 32-bit signed integer range:
   - `[-2^31, 2^31 - 1]`

If no valid conversion can be performed, return `0`.

---

## 🛠️ Approach

1. **Skip leading spaces**  
   Move the pointer forward until a non-space character is found.

2. **Check sign**  
   If the current character is `+` or `-`, store the sign and move ahead.

3. **Convert digits**  
   - Iterate while characters are digits.
   - Build the number using `result = result * 10 + digit`.

4. **Handle overflow early**  
   - If value exceeds `INT_MAX` or `INT_MIN`, return the respective limit immediately.

5. **Return final result**  
   Multiply by sign and return.

---

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(1)`

---

## 💻 C++ Code

```cpp
class Solution {
public:
    int myAtoi(string s) {
        long long result = 0;
        int i = 0;
        int sign = 1;
        int n = s.size();

        // Skip leading spaces
        while (i < n && s[i] == ' ')
            i++;

        // Check sign
        if (i < n && (s[i] == '+' || s[i] == '-')) {
            if (s[i] == '-')
                sign = -1;
            i++;
        }

        // Convert digits
        while (i < n && isdigit(s[i])) {
            result = result * 10 + (s[i] - '0');

            if (result * sign > INT_MAX)
                return INT_MAX;
            if (result * sign < INT_MIN)
                return INT_MIN;

            i++;
        }

        return (int)(result * sign);
    }
};


Example Walkthrough
Input
"   -42"

Output
-42

**Explanation**

Leading spaces ignored

- detected → sign = -1

Digits read → 42

Final answer → -42

✅ Key Takeaways

Always handle overflow before returning

Stop parsing when a non-digit appears

Edge cases matter more than logic here
