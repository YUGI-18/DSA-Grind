# 🔁 Implement Queue using Stacks

## 📝 Problem Statement

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

### Class: `MyQueue`

* `void push(int x)`: Pushes element `x` to the back of the queue.
* `int pop()`: Removes the element from the front of the queue and returns it.
* `int peek()`: Returns the element at the front of the queue.
* `boolean empty()`: Returns `true` if the queue is empty, `false` otherwise.

### Notes:

* Only standard stack operations are allowed: push to top, peek/pop from top, size, and isEmpty.

---

## ✨ Example

### Example 1:

**Input:**

```cpp
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**Output:**

```cpp
[null, null, null, 1, 1, false]
```

**Explanation:**

```cpp
MyQueue myQueue = new MyQueue();
myQueue.push(1);       // queue is: [1]
myQueue.push(2);       // queue is: [1, 2]
myQueue.peek();        // return 1
myQueue.pop();         // return 1, queue becomes [2]
myQueue.empty();       // return False
```

---

## 🚀 Approach

* Use two stacks: `st1` (input stack) and `st2` (output stack).
* For `push(x)`: Push to `st1`.
* For `pop()` and `peek()`: If `st2` is empty, transfer all elements from `st1` to `st2` (reverse the order).
* For `empty()`: Return true only if both stacks are empty.

---

## 🔢 Code Implementation

```cpp
class MyQueue {
public:
    stack<int> st1;
    stack<int> st2;

    MyQueue() {}

    void push(int x) {
        st1.push(x);
    }

    int pop() {
        if (st2.empty()) {
            while (!st1.empty()) {
                st2.push(st1.top());
                st1.pop();
            }
        }
        int popped = st2.top();
        st2.pop();
        return popped;
    }

    int peek() {
        if (st2.empty()) {
            while (!st1.empty()) {
                st2.push(st1.top());
                st1.pop();
            }
        }
        return st2.top();
    }

    bool empty() {
        return st1.empty() && st2.empty();
    }
};
```

---

## ⏱ Time Complexity

* `push`: O(1)
* `pop`: Amortized O(1)
* `peek`: Amortized O(1)
* `empty`: O(1)

## 💾 Space Complexity

* O(n) — Space used by the two stacks.

---

## 🌟 Key Points

* Simulates queue behavior using two stacks.
* Amortized O(1) performance for main operations.
* Efficient and commonly used in interview questions.
