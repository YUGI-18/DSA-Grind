# ⚡ Quick Sort Implementation

## Problem Statement

Implement Quick Sort, a Divide and Conquer algorithm, to sort an array, `arr[]`, in ascending order. Given an array, `arr[]`, with starting index `low` and ending index `high`, complete the functions `partition()` and `quickSort()`. Use the **last element** as the pivot so that all elements less than or equal to the pivot come before it, and elements greater than the pivot follow it.

**Note:** The `low` and `high` indices are inclusive.

---

## 🎯 Objective

Sort an array in ascending order using the Quick Sort algorithm.

---

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
arr[] = [2, 1, 6, 10, 4, 1, 3, 9, 7]
```
**Output:**
```cpp
[1, 1, 2, 3, 4, 6, 7, 9, 10]
```

### Example 3:

**Input:**
```cpp
arr[] = [5, 5, 5, 5]
```
**Output:**
```cpp
[5, 5, 5, 5]
```

---

## 🚀 Approach: Lomuto Partition Scheme

### *Algorithm*

1. Choose the last element as the pivot.
2. Partition the array so that all elements smaller than or equal to the pivot are on the left, and larger elements are on the right.
3. Recursively sort the left and right partitions.

### *Time Complexity*:
- **Best & Average Case:** O(n log n)
- **Worst Case:** O(n^2)

---

## 🔢 Code Implementation

```cpp
class Solution {
  public:
    void quickSort(vector<int>& arr, int low, int high) {
        if (low < high) {
            int part = partition(arr, low, high);
            quickSort(arr, low, part - 1);
            quickSort(arr, part + 1, high);
        }
    }

    int partition(vector<int>& arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr[i], arr[j]);
            }
        }
        swap(arr[i + 1], arr[high]);
        return i + 1;
    }
};
```

---

## 🔧 Constraints

- `1 <= arr.size() <= 10^5`
- `1 <= arr[i] <= 10^5`

---

## 🌟 Key Points

- Quick Sort is an in-place sorting algorithm.
- Efficient in practice for large datasets.
- Utilizes a divide and conquer strategy.
- Lomuto partition scheme is used here for clarity.

---

## 🛠 How to Run

1. Clone this repository:
   ```sh
   git clone https://github.com/your-username/quick-sort.git
   ```
2. Navigate to the project directory:
   ```sh
   cd quick-sort
   ```
3. Compile and run the C++ program:
   ```sh
   g++ -o quick_sort quick_sort.cpp
   ./quick_sort
   ```

---
