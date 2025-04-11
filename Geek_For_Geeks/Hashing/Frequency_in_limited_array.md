# 📊 Frequencies in a Limited Array

## Problem Statement

You are given an array `arr[]` containing positive integers. The elements in the array range from 1 to `n` (where `n` is the size of the array). Some numbers may be repeated or absent.

Your task is to count the frequency of all numbers in the range `1` to `n` and return an array of size `n` such that `result[i]` represents the frequency of the number `i + 1` (1-based indexing).

---

## 🎯 Objective

Count the frequency of each number in the array from 1 to `n`.

---

## ✨ Examples

### Example 1:

**Input:**
```cpp
arr[] = [2, 3, 2, 3, 5]
```

**Output:**
```cpp
[0, 2, 2, 0, 1]
```

**Explanation:**
- 1 occurs 0 times
- 2 occurs 2 times
- 3 occurs 2 times
- 4 occurs 0 times
- 5 occurs 1 time

### Example 2:

**Input:**
```cpp
arr[] = [3, 3, 3, 3]
```

**Output:**
```cpp
[0, 0, 4, 0]
```

**Explanation:**
- 1 occurs 0 times
- 2 occurs 0 times
- 3 occurs 4 times
- 4 occurs 0 times

### Example 3:

**Input:**
```cpp
arr[] = [1]
```

**Output:**
```cpp
[1]
```

**Explanation:**
- 1 occurs 1 time

---

## 🚀 Approach: Frequency Count with Index Mapping

### *Algorithm*

1. Initialize a result array of size `n` filled with zeros.
2. Iterate through the input array:
   - For each number `x` in the array, increment the count at `result[x - 1]`.
3. Return the result array.

### *Time Complexity*:
- **O(n)** where `n` is the size of the array.

### *Space Complexity*:
- **O(n)** for the result array.

### Code Implementation

```cpp
class Solution {
  public:
    // Function to count the frequency of all elements from 1 to N in the array.
    vector<int> frequencyCount(vector<int>& arr) {
        int len = arr.size();
        vector<int> freq(len);
        for (int i = 0; i < len; i++) {
            freq[arr[i] - 1] += 1;
        }
        return freq;
    }
};
```

---

## 🔧 Constraints

- `1 ≤ arr.size() ≤ 10^6`
- `1 ≤ arr[i] ≤ arr.size()`

---

## 🌟 Key Points

- Efficiently counts how many times each number appears in the array.
- Uses 0-based indexing to store frequencies.
- Ensures correct count even with duplicates or missing elements.

---

## 🔗 Related Topics
- Arrays
- Hashing
- Counting Algorithms

