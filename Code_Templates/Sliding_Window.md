
### 📘 Sliding Window Templates

This section contains reusable C++ templates for solving problems using the **sliding window technique**, categorized into fixed-size and variable-size patterns.

---

### 📏 Fixed Size Sliding Window

```cpp
int fn(vector<int>& arr, int k) {
    int left = 0, curr = 0, ans = 0;

    for (int right = 0; right < arr.size(); right++) {
        // Add arr[right] to curr
        curr += arr[right];

        // If window size > k, shrink from left
        if (right - left + 1 > k) {
            curr -= arr[left];
            left++;
        }

        // If window size == k, update ans
        if (right - left + 1 == k) {
            ans = max(ans, curr); // or some logic
        }
    }

    return ans;
}
```

---

**🟦 Use When:**

* The window size `k` is **fixed or given**.
* You need to find:

  * Max/Min sum of subarrays of size `k`
  * Count of patterns in a window of constant size

---

**🛠 Inbuilt Equivalent:** ❌ Manual implementation needed.
STL `deque` can help for optimized versions (e.g., max sliding window).

---

### 📐 Variable Size Sliding Window

```cpp
int fn(vector<int>& arr) {
    int left = 0, ans = 0, curr = 0;

    for (int right = 0; right < arr.size(); right++) {
        // Add arr[right] to curr
        curr += arr[right];

        while (WINDOW_CONDITION_BROKEN) {
            // Remove arr[left] from curr
            curr -= arr[left];
            left++;
        }

        // Update ans (can be max length, count, etc.)
        ans = max(ans, right - left + 1); // or other logic
    }

    return ans;
}
```

---

**🟦 Use When:**

* The window size is **dynamic** — it depends on a condition.
* You're solving problems like:

  * Longest subarray with sum ≤ K
  * Longest substring without repeating characters
  * Count of subarrays with at most K distinct integers

---

**🛠 Inbuilt Equivalent:** ❌ Manual loop control required.

---
