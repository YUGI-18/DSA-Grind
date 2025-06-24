
### 📘 Stack Templates

This section contains standard stack-based templates in C++ for solving problems involving **monotonic properties**, like Next Greater Element, Histogram Area, and more.

---

### 📈 Monotonic Increasing Stack

```cpp
int fn(vector<int>& arr) {
    stack<int> stack;
    int ans = 0;

    for (int num : arr) {
        // For monotonic decreasing stack, change '>' to '<'
        while (!stack.empty() && stack.top() > num) {
            // do logic
            stack.pop();
        }

        stack.push(num);
    }

    return ans;
}
```

---

**🟦 Use When:**

* You need to maintain a **monotonic increasing or decreasing order** to solve problems like:

  * Finding **next smaller/greater** elements
  * Computing **spans** or **ranges**
  * Solving **histogram area** problems
  * Processing **daily temperatures**, stock prices, etc.

---

**🔁 Monotonic Stack Variants:**

* **Monotonic Increasing Stack**:

  * Keeps elements in **increasing order**
  * Useful for **next smaller**, **previous smaller**
* **Monotonic Decreasing Stack**:

  * Change `>` to `<`
  * Useful for **next greater**, **previous greater**

---

**🛠 Inbuilt Equivalent:** ❌ No STL inbuilt — must be implemented manually.

---

### 🔍 Common Use Cases:

| Problem                            | Stack Type           | Logic Inside `while`                             |
| ---------------------------------- | -------------------- | ------------------------------------------------ |
| **Next Greater Element**           | Monotonic decreasing | Compare top with current; store index difference |
| **Next Smaller Element**           | Monotonic increasing | Same pattern                                     |
| **Daily Temperatures**             | Monotonic decreasing | Store indices; calculate days difference         |
| **Largest Rectangle in Histogram** | Both                 | Pop and calculate area using width               |

---

### 📦 Stack: Matching / Sequence Validation

```cpp
for (char c : input_string) {
    stack<char> stack;
    stack.push(c);

    if (specific_condition_is_met) {
        while (!stack.empty() && some_condition) {
            if (stack.top() != expected_value) {
                return false; // Invalid sequence
            }
            stack.pop();
        }
    }
}
return stack.empty() ? true : false;
```

---

**🟦 Use When:**

* You're validating **nested structures**, such as:

  * **Parentheses/brackets**: `()`, `{}`, `[]`
  * **Backspace/Undo** logic
  * **Balanced sequences**, or proper matching tags
* Common in:

  * **Valid Parentheses** (LC 20)
  * **Remove All Adjacent Duplicates** (LC 1047)
  * **Backspace String Compare** (LC 844)

---

**🛠 Inbuilt Equivalent:** ❌ No direct STL

* Use `std::stack<char>` manually.

---

### 🔍 Key Idea:

* Use a stack to simulate a **processing machine**.
* Push characters until a **specific pattern** appears.
* Then use a loop to **validate and remove** matching elements.

---
