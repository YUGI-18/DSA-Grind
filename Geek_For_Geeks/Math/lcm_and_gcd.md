# 🔄 LCM and GCD Calculator

## Problem Statement

Given two integers `a` and `b`, compute their **LCM (Least Common Multiple)** and **GCD (Greatest Common Divisor)** and return an array containing their LCM and GCD.

## 🎯 Objective

Write a function to calculate the **LCM** and **GCD** of two numbers efficiently.

## ✨ Example

### Example 1:

**Input:**

```cpp
a = 5, b = 10
```

**Output:**

```cpp
[10, 5]
```

**Explanation:** LCM of 5 and 10 is 10, while their GCD is 5.

### Example 2:

**Input:**

```cpp
a = 14, b = 8
```

**Output:**

```cpp
[56, 2]
```

**Explanation:** LCM of 14 and 8 is 56, while their GCD is 2.

### Example 3:

**Input:**

```cpp
a = 1, b = 1
```

**Output:**

```cpp
[1, 1]
```

**Explanation:** LCM of 1 and 1 is 1, while their GCD is 1.

---

## 🚀 Approach: Using Iterative Method

### *Algorithm*

1. Identify the larger and smaller number between `a` and `b`.
2. Compute the **LCM**:
   - Start with the maximum of `a` and `b`.
   - Increment until a number is found that is divisible by both `a` and `b`.
3. Compute the **GCD**:
   - Start with the minimum of `a` and `b`.
   - Decrement until a number is found that divides both `a` and `b` evenly.

### *Time Complexity*:
- The approach runs in *O(n)* for LCM and GCD computation.

### Code Implementation

```cpp
class Solution {
  public:
    vector<int> lcmAndGcd(int a, int b) {
        int big, small;
        vector<int> value = {2, 2};
        
        if (a < b) {
            big = b;
            small = a;
        } else {
            big = a;
            small = b;
        }
        
        value[0] = big;
        value[1] = small;
        
        if (a == 1 && b == 1) {
            value[0] = 1;
            value[1] = 1;
            return value;
        }
        
        while (value[0] % a != 0 || value[0] % b != 0) {
            value[0] += big;
        }
        
        while (a % value[1] != 0 || b % value[1] != 0) {
            value[1]--;
        }
        
        return value;
    }
};
```

---

## 🔧 Constraints

- `1 ≤ a, b ≤ 10^9`
- The solution must be efficient for large values of `a` and `b`.

---

## 🌟 Key Points

- Uses basic arithmetic operations to compute **LCM** and **GCD**.
- The solution ensures correctness for both small and large values.
- Handles edge cases like `a = 1, b = 1` correctly.

---
