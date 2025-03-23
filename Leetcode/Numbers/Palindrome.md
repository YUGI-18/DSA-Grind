
# 🔄 Palindrome Number Checker

## Problem Statement

Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

## 🎯 Objective

Write a function to determine whether a given integer is a palindrome.

## ✨ Example

### Example 1:

**Input:**

```cpp
x = 121
```

**Output:**

```cpp
true
```

**Explanation:** 121 reads as 121 from left to right and from right to left.

### Example 2:

**Input:**

```cpp
x = -121
```

**Output:**

```cpp
false
```

**Explanation:** From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

### Example 3:

**Input:**

```cpp
x = 10
```

**Output:**

```cpp
false
```

**Explanation:** Reads 01 from right to left. Therefore, it is not a palindrome.

---

## 🚀 Approach: Two-Pointer Technique

### *Algorithm*

1. Convert the given integer `x` into a string.
2. Use two pointers, one starting from the beginning and the other from the end.
3. Compare the characters at both pointers:
   - If they are equal, move both pointers towards the center.
   - If they are not equal, return `false`.
4. If all characters match, return `true`.

### *Time Complexity*:
- The algorithm runs in *O(n)* time, where `n` is the length of the string.

### Code Implementation

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        string val = to_string(x);
        int start = 0;
        int end = val.length() - 1;
        
        while (start <= end) {
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

- `-2^{31} ≤ x ≤ 2^{31} - 1`
- The solution must be efficient for large integers.

---

## 🌟 Key Points

- The solution converts the integer into a string and uses two pointers for comparison.
- It ensures an *O(n)* time complexity for efficient execution.
- Works efficiently for both positive and negative integers but immediately returns `false` for negative values.
- The implementation is straightforward and easy to understand.

---



