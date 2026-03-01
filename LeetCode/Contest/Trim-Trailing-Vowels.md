# Q1. Trim Trailing Vowels

## 🟢 Problem Summary

You are given a string `s` consisting of lowercase English letters.

Return the string obtained after **removing all trailing vowels** from `s`.

Vowels are:
'a' , 'e' , 'i' , 'o', 'u'


---

## 🧠 Key Idea

We only care about **vowels at the end** of the string.

So:
- Start from the last character.
- Move backwards while the character is a vowel.
- Return the substring up to the last non-vowel.

This is an **O(n)** solution.

---

## ✨ Example


### Example 1

Input:
```
s = "idea"
```

Process:
- 'a' → vowel → remove
- 'e' → vowel → remove```
- stop at 'd'

Output:    
```
"id"
```

---

### Example 2

Input:
```
s = "day"
```

Last character is `'y'` (not a vowel).

Output:
```
"day"
```


---

## 💻 C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string trimTrailingVowels(string s) {
        int i = s.length() - 1;

        while (i >= 0 && isVowel(s[i])) {
            i--;
        }

        return s.substr(0, i + 1);
    }

private:
    bool isVowel(char c) {
        return (c == 'a' || c == 'e' || c == 'i' ||
                c == 'o' || c == 'u');
    }
};
```
## Complexity

- Time: O(n)

- Space: O(1)
