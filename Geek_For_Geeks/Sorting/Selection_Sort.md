# 🔃 Selection Sort

## Problem Statement

Given an array `arr`, use **selection sort** to sort the elements in increasing order.

## ✨ Example

### Example 1:

**Input:**
```cpp
arr[] = [4, 1, 3, 9, 7]
```
**Output:**
```cpp
[1, 3, 4, 7, 9]
```
**Explanation:**
- Select 1. Array becomes [1, 4, 3, 9, 7]
- Select 3. Array becomes [1, 3, 4, 9, 7]
- Select 4. Already in place.
- Select 7. Array becomes [1, 3, 4, 7, 9]
- Select 9. Already in place.

### Example 2:

**Input:**
```cpp
arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```
**Output:**
```cpp
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Example 3:

**Input:**
```cpp
arr[] = [38, 31, 20, 14, 30]
```
**Output:**
```cpp
[14, 20, 30, 31, 38]
```

---

## 🚀 Approach: Selection Sort

### *Algorithm*
1. Iterate from the beginning of the array to the second last element.
2. For each position `i`, find the smallest element in the unsorted part (`i` to end).
3. Swap the smallest element with the element at position `i`.
4. Repeat until the entire array is sorted.

### *Time Complexity*:
- Best, Average, and Worst Case: **O(n²)**
- Space Complexity: **O(1)** (In-place sort)

### Code Implementation

```cpp
class Solution {
  public:
    // Function to perform selection sort on the given array.
    void selectionSort(vector<int> &arr) {
        int len = arr.size();
        int temp, min;
        for (int i = 0; i <= len - 2; i++) {
            min = i;
            for (int j = i; j <= len - 1; j++) {
                if (arr[min] > arr[j]) {
                    min = j;
                }
            }
            temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }
};
```

---

## 🔧 Constraints
- `1 ≤ arr.size() ≤ 10^3`
- `1 ≤ arr[i] ≤ 10^6`

---

## 📊 Key Points
- Selection sort repeatedly finds the minimum element from the unsorted part.
- Good for educational purposes but inefficient for large datasets.
- In-place sorting (no extra space needed).

---
