# 🔄 Reverse Integer

## Problem Statement

Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^{31}, 2^{31} - 1]`, then return `0`.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

## 🎯 Objective

Write a function to reverse the digits of an integer while handling overflow conditions.

## ✨ Example

### Example 1:

**Input:**

```cpp
x = 123
```

**Output:**

```cpp
321
```

### Example 2:

**Input:**

```cpp
x = -123
```

**Output:**

```cpp
-321
```

### Example 3:

**Input:**

```cpp
x = 120
```

**Output:**

```cpp
21
```

---

## 🚀 Approach: Digit Extraction and Overflow Handling

### *Algorithm*

1. Extract each digit of `x` using the modulo operator (`% 10`).
2. Build the reversed number by multiplying the current result by `10` and adding the extracted digit.
3. Handle integer overflow by checking if the reversed number exceeds the 32-bit integer range.
4. Return `0` if an overflow occurs; otherwise, return the reversed integer.

### *Time Complexity*:
- The algorithm runs in *O(log n)* time since it processes each digit of `x`.

### Code Implementation

```cpp
class Solution {
public:
    int reverse(int x) {
        int num = x;
        int rem;
        long res = 0;
        
        while (num != 0) {
            rem = num % 10;
            num = num / 10;
            res = res * 10 + rem;
        }
        
        if (res >= INT_MAX || res <= INT_MIN) return 0;
        
        return res;
    }
};
```

---

## 🔧 Constraints

- `-2^{31} ≤ x ≤ 2^{31} - 1`
- The solution efficiently handles overflow conditions.

---

## 🌟 Key Points

- Uses basic arithmetic operations for optimal performance.
- Handles negative numbers correctly.
- Ensures no integer overflow by checking limits before returning the result.
- The complexity is logarithmic in terms of digits processed.

---
