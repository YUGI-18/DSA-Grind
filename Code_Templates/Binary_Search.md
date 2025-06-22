
# 📘 Binary Search Templates (C++)

This document contains commonly used **binary search patterns** in C++ that you can reuse across different problems. These templates are essential for problems involving sorted arrays, optimization via monotonic behavior, and more.

---

### 🔍 1. Binary Search: Basic Form

```cpp
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = int(arr.size()) - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            // do something
            return mid;
        }
        if (arr[mid] > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }

    // Target not found — return insertion point
    return left;
}
```

**🟦 Use When:**

* You want to **find the exact position** of a target in a sorted array.
* Works well for problems like:

  * Search target index
  * Search Insert Position

**🛠 Inbuilt Equivalent:** `std::binary_search(arr.begin(), arr.end(), target)` (returns bool only)
Use `std::lower_bound()` or `std::upper_bound()` for index.

---

### 📌 2. Binary Search: Left-most Insertion Point (Lower Bound)

```cpp
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size();

    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] >= target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

**🟦 Use When:**

* You want to find the **first position where target can be inserted**.
* Returns the index of the **first element ≥ target**.
* Use cases:

  * Lower bound search
  * Count of elements `< target` → index itself

**🛠 Inbuilt Equivalent:** `std::lower_bound(arr.begin(), arr.end(), target) - arr.begin()`

---

### 📌 3. Binary Search: Right-most Insertion Point (Upper Bound)

```cpp
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size();

    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] > target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

**🟦 Use When:**

* You want to find the **last position where target can be inserted**.
* Returns the index of the **first element > target**.
* Use cases:

  * Upper bound search
  * Count of elements ≤ target → index itself

**🛠 Inbuilt Equivalent:** `std::upper_bound(arr.begin(), arr.end(), target) - arr.begin()`

---

### 🔄 4. Binary Search: Search in Rotated Sorted Array

```cpp
int search(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) return mid;

        // Left half is sorted
        if (arr[left] <= arr[mid]) {
            if (arr[left] <= target && target < arr[mid])
                right = mid - 1;
            else
                left = mid + 1;
        }
        // Right half is sorted
        else {
            if (arr[mid] < target && target <= arr[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }

    return -1;
}
```

**🟦 Use When:**

* The array is **rotated at some pivot** but still sorted in segments.
* You need to search a target efficiently in such rotated arrays.
* Common in:

  * LeetCode 33: Search in Rotated Sorted Array

**🛠 Inbuilt Equivalent:** ❌ No direct STL equivalent
Must be implemented manually.

---

### 📈 5. Binary Search on Answer (Search Space Binary Search)

```cpp
int fn(vector<int>& arr) {
    int low = 0;
    int high = 1e9;
    int ans = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (isValid(mid, arr)) {
            ans = mid;
            high = mid - 1; // or low = mid + 1 depending on min/max goal
        } else {
            low = mid + 1;
        }
    }

    return ans;
}
```

**🟦 Use When:**

* The array isn’t sorted, but you're optimizing over a **monotonic value space**.
* You define a helper like `isValid(mid)` to check feasibility.
* Common in:

  * Min/max days
  * Resource allocation
  * Koko Eating Bananas, Capacity to Ship Packages, etc.

**🛠 Inbuilt Equivalent:** ❌ No STL equivalent
Must be implemented with custom `isValid()` logic.

---

### 🧮 6. Binary Search in 2D Matrix

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (matrix.empty() || matrix[0].empty()) return false;

    int m = matrix.size();
    int n = matrix[0].size();
    int left = 0, right = m * n - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        int val = matrix[mid / n][mid % n];

        if (val == target) return true;
        else if (val < target) left = mid + 1;
        else right = mid - 1;
    }

    return false;
}
```

**🟦 Use When:**

* You have a 2D matrix where:

  * Each row is sorted
  * First element of each row > last element of previous row
* Matrix can be treated as a 1D array for binary search.
* Common in:

  * LeetCode 74: Search a 2D Matrix

**🛠 Inbuilt Equivalent:** ❌ No direct STL
But can simulate using `std::binary_search` with custom accessors.

---
