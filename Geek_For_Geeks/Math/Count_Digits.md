# 🔢 Evenly Dividing Digits

## Problem Statement

Given a positive integer `n`, count the number of digits in `n` that divide `n` evenly (i.e., without leaving a remainder). Return the total number of such digits.

A digit `d` of `n` divides `n` evenly if the remainder when `n` is divided by `d` is `0` (`n % d == 0`).
Digits of `n` should be checked individually. If a digit is `0`, it should be ignored because division by `0` is undefined.

## 🎯 Objective

Write a function to count the number of digits in `n` that evenly divide `n`.

## ✨ Example

### Example 1:

**Input:**

```cpp
n = 12
```

**Output:**

```cpp
2
```

**Explanation:** 1 and 2 both divide 12 evenly.

### Example 2:

**Input:**

```cpp
n = 2446
```

**Output:**

```cpp
1
```

**Explanation:** Among 2, 4, and 6, only 2 divides 2446 evenly, while 4 and 6 do not.

### Example 3:

**Input:**

```cpp
n = 23
```

**Output:**

```cpp
0
```

**Explanation:** Neither 2 nor 3 divides 23 evenly.

---

## 🚀 Approach: Digit Extraction and Modulo Check

### *Algorithm*

1. Extract each digit from `n` by repeatedly using the modulo operator (`% 10`).
2. Check if the digit is not `0` to avoid division errors.
3. If `n % digit == 0`, increment the count.
4. Continue until all digits are checked.
5. Return the final count.

### *Time Complexity*:
- The algorithm runs in *O(d)* time, where `d` is the number of digits in `n`.

### Code Implementation

```cpp
class Solution {
  public:
    // Function to count the number of digits in n that evenly divide n
    int evenlyDivides(int n) {
        int num = n;
        int rem;
        int val = 0;
        while (num != 0) {
            rem = num % 10;
            num = num / 10;
            if (rem != 0) {
                if (n % rem == 0) {
                    val++;
                }
            }
        }
        return val;
    }
};
```

---

## 🔧 Constraints

- `1 ≤ n ≤ 10^5`
- The solution efficiently processes numbers up to five digits.

---

## 🌟 Key Points

- The solution iterates through each digit of `n`.
- It ensures division by zero is avoided.
- The complexity is proportional to the number of digits in `n`, making it efficient.
- Uses basic arithmetic operations for optimal performance.

---
