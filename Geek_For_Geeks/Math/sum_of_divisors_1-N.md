# 🔢 Sum of Divisors from 1 to n

## Problem Statement

Given a positive integer `n`, the task is to find the value of:

\[ \sum_{i=1}^{n} F(i) \]

where function `F(i)` is defined as the sum of all divisors of `i`.

## 🎯 Objective

Write a function that computes the sum of divisors for all numbers from `1` to `n`.

## ✨ Example

### Example 1:

**Input:**

```cpp
n = 4
```

**Output:**

```cpp
15
```

**Explanation:**
```
F(1) = 1
F(2) = 1 + 2 = 3
F(3) = 1 + 3 = 4
F(4) = 1 + 2 + 4 = 7
Total sum = 1 + 3 + 4 + 7 = 15
```

### Example 2:

**Input:**

```cpp
n = 5
```

**Output:**

```cpp
21
```

**Explanation:**
```
F(1) = 1
F(2) = 1 + 2 = 3
F(3) = 1 + 3 = 4
F(4) = 1 + 2 + 4 = 7
F(5) = 1 + 5 = 6
Total sum = 1 + 3 + 4 + 7 + 6 = 21
```

---

## 🚀 Approach: Brute Force Calculation

### *Algorithm*

1. Initialize `sum = 0`.
2. Iterate through all numbers from `1` to `n`.
3. For each number `i`, find all divisors and sum them up.
4. Accumulate this sum into a global sum.
5. Return the final sum.

### *Time Complexity*:
- The algorithm runs in *O(n^2)* time due to nested loops.

### Code Implementation

```cpp
class Solution {
  public:
    int sumOfDivisors(int n) {
        int sum = 0;
        
        if (n == 1) return 1;
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                if (i % j == 0) {
                    sum += j;
                }
            }
        }
        return sum;
    }
};
```

---

## 🔧 Constraints

- `1 ≤ n ≤ 10^5`
- The function should be optimized for larger values of `n`.

---


