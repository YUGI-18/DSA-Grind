
#### 🔁 Two Pointers: One Input, Opposite Ends

```cpp
int fn(vector<int>& arr) {
    int left = 0;
    int right = int(arr.size()) - 1;
    int ans = 0;

    while (left < right) {
        // do some logic here with left and right
        if (CONDITION) {
            left++;
        } else {
            right--;
        }
    }

    return ans;
}
```

**🔹 Use When:**

* You need to process elements from both ends toward the middle.
* Problems like: **Two Sum (sorted)**, **Container With Most Water**, **Valid Palindrome**.

---

#### 🔁 Two Pointers: Two Inputs, Exhaust Both

```cpp
int fn(vector<int>& arr1, vector<int>& arr2) {
    int i = 0, j = 0, ans = 0;

    while (i < arr1.size() && j < arr2.size()) {
        // do some logic here
        if (CONDITION) {
            i++;
        } else {
            j++;
        }
    }

    while (i < arr1.size()) {
        // do logic
        i++;
    }

    while (j < arr2.size()) {
        // do logic
        j++;
    }

    return ans;
}
```

**🔹 Use When:**

* You need to iterate through **two sorted arrays/lists** and perform operations like merge, intersection, or comparison.
* Problems like: **Merge Two Sorted Lists**, **Intersection of Two Arrays**, **Sorted Array Merge**.

**🔹 How to Use:**

* Replace `CONDITION` with a comparison logic (e.g., `arr1[i] < arr2[j]`).
* Fill in logic inside each loop for the problem-specific operation.

---
