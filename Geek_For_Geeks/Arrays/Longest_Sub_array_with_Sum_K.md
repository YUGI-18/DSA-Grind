# 📏 Longest Subarray with Sum K

## Problem Statement

Given an array `arr[]` containing integers and an integer `k`, your task is to find the length of the **longest subarray** where the sum of its elements is equal to the given value `k`. If there is no subarray with sum equal to `k`, return `0`.

---

## 🎯 Objective

Return the maximum length of a contiguous subarray such that the sum of the elements is equal to `k`.

---

## ✨ Examples

### Example 1:

**Input:**
```cpp
arr[] = [10, 5, 2, 7, 1, -10], k = 15
```
**Output:**
```cpp
6
```
**Explanation:** The longest subarray is [10, 5, 2, 7, 1, -10] with a sum of 15.

### Example 2:

**Input:**
```cpp
arr[] = [-5, 8, -14, 2, 4, 12], k = -5
```
**Output:**
```cpp
5
```
**Explanation:** Only subarray with sum = -5 is [-5, 8, -14, 2, 4].

### Example 3:

**Input:**
```cpp
arr[] = [10, -10, 20, 30], k = 5
```
**Output:**
```cpp
0
```
**Explanation:** No subarray found with sum = 5.

---

## 🚀 Approach: Prefix Sum with Hash Map

### *Algorithm*

1. Use a hash map `presum` to store the first occurrence of each prefix sum.
2. Traverse the array while maintaining the cumulative sum.
3. If `sum == k`, update the maximum length.
4. If `(sum - k)` exists in the map, a subarray with sum `k` is found.
5. Insert `sum` into the map if it’s not already present.

### *Time Complexity*:
- **O(n)** — Single pass through the array.

### *Space Complexity*:
- **O(n)** — For storing prefix sums.

---

## 🔢 Code Implementation

```cpp
class Solution {
  public:
    int longestSubarray(vector<int>& arr, int k) {
        map<long long, int> presum;
        long long sum = 0;
        int maxlen = 0;

        for (int i = 0; i < arr.size(); i++) {
            sum += arr[i];

            if (sum == k) {
                maxlen = max(maxlen, i + 1);
            }

            long long rem = sum - k;
            if (presum.find(rem) != presum.end()) {
                int len = i - presum[rem];
                maxlen = max(maxlen, len);
            }

            if (presum.find(sum) == presum.end()) {
                presum[sum] = i;
            }
        }
        return maxlen;
    }
};
```

---

## 🔧 Constraints

- `1 <= arr.size() <= 10^5`
- `-10^4 <= arr[i] <= 10^4`
- `-10^9 <= k <= 10^9`

---

## 🌟 Key Points

- Efficient use of prefix sums to handle both positive and negative values.
- Hash map ensures fast lookup for previous prefix sums.
- Handles large input sizes efficiently.

---
