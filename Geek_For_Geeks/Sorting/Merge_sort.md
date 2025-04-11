# 🧩 Merge Sort Algorithm

## Problem Statement

Given an array `arr[]`, its starting position `l`, and its ending position `r`, sort the array using the **Merge Sort** algorithm.

## ✨ Examples

### Example 1:
**Input:**
```cpp
arr[] = [4, 1, 3, 9, 7]
```
**Output:**
```cpp
[1, 3, 4, 7, 9]
```

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
arr[] = [1, 3, 2]
```
**Output:**
```cpp
[1, 2, 3]
```

---

## 🚀 Approach: Merge Sort

### *Algorithm*

1. Divide the array into two halves.
2. Recursively sort the two halves.
3. Merge the sorted halves into a single sorted array.

### *Time Complexity*:
- **O(n log n)** — where `n` is the number of elements in the array.

### *Space Complexity*:
- **O(n)** for temporary arrays used during merging.

---

## 📄 Code Implementation

```cpp
class Solution {
  public:
    void merge(vector<int>& arr, int l, int mid, int r) {
        int left = l;
        int right = mid + 1;
        vector<int> temp;

        while (left <= mid && right <= r) {
            if (arr[left] < arr[right]) {
                temp.push_back(arr[left]);
                left++;
            } else {
                temp.push_back(arr[right]);
                right++;
            }
        }

        while (left <= mid) {
            temp.push_back(arr[left]);
            left++;
        }

        while (right <= r) {
            temp.push_back(arr[right]);
            right++;
        }

        for (int i = l; i <= r; i++) {
            arr[i] = temp[i - l];
        }
    }

    void mergeSort(vector<int>& arr, int l, int r) {
        if (l == r) return;
        int mid = (l + r) / 2;
        mergeSort(arr, l, mid);
        mergeSort(arr, mid + 1, r);
        merge(arr, l, mid, r);
    }
};
```

---

## 🔧 Constraints

- `1 <= arr.size() <= 10^5`
- `1 <= arr[i] <= 10^5`

---

## 💡 Key Points
- Divide and conquer technique.
- Efficient for large datasets.
- Stable sort: maintains relative order of equal elements.

---
