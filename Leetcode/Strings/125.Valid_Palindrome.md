# 🔄 Valid Palindrome Checker

## Problem Statement
A phrase is a palindrome if, after converting all uppercase letters into lowercase and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

## 🎯 Objective
Write a function to check whether a given string is a valid palindrome after removing non-alphanumeric characters and ignoring case.

## ✨ Example

### Example 1:

**Input:**

```cpp
s = "A man, a plan, a canal: Panama"
```

**Output:**

```cpp
true
```

**Explanation:** "amanaplanacanalpanama" is a palindrome.

### Example 2:

**Input:**

```cpp
s = "race a car"
```

**Output:**

```cpp
false
```

**Explanation:** "raceacar" is not a palindrome.

### Example 3:

**Input:**

```cpp
s = " "
```

**Output:**

```cpp
true
```

**Explanation:** After removing non-alphanumeric characters, `s` is an empty string "", which is a palindrome.

---

## 🚀 Approach: Two-Pointer Technique

### *Algorithm*

1. Initialize an empty string `val`.
2. Traverse through `s` and keep only alphanumeric characters, converting them to lowercase.
3. Use two pointers: one at the start and one at the end of `val`.
4. Compare characters at both pointers:
   - If they are different, return `false`.
   - If they match, move both pointers towards the center.
5. If all characters match, return `true`.

### *Time Complexity*:
- The algorithm runs in *O(n)* time, where `n` is the length of the string.

### Code Implementation

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        string val;
        for (char c : s) {
            if (isalnum(c)) val += tolower(c);
        }
        int start = 0, end = val.length() - 1;
        
        while (start < end) {
            if (val[start] != val[end]) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
};
```

---

## 🔧 Constraints

- `1 <= s.length <= 2 * 10^5`
- `s` consists only of printable ASCII characters.

---
