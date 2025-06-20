# 🔁 Implement Stack using Queues

## 📝 Problem Statement

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

### Class: `MyStack`

* `void push(int x)`: Pushes element `x` to the top of the stack.
* `int pop()`: Removes the element on the top of the stack and returns it.
* `int top()`: Returns the element on the top of the stack.
* `boolean empty()`: Returns `true` if the stack is empty, `false` otherwise.

### Notes:

* Only standard operations of a queue are allowed: push to back, peek/pop from front, size, and isEmpty.

---

## ✨ Example

### Example 1:

**Input:**

```cpp
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**Output:**

```cpp
[null, null, null, 2, 2, false]
```

**Explanation:**

```cpp
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top();    // return 2
myStack.pop();    // return 2
myStack.empty();  // return False
```

---

## 🚀 Approach

* Maintain a single queue.
* On each `push(x)`, insert `x` and rotate the queue to bring it to the front.
* `pop()` simply dequeues the front.
* `top()` peeks at the front.
* `empty()` checks if the queue is empty.

---

## 🔢 Code Implementation

```cpp
class MyStack {
public:
    queue<int> q;

    MyStack() {
        // Constructor
    }

    void push(int x) {
        int s = q.size();
        q.push(x);
        for (int i = 0; i < s; i++) {
            q.push(q.front());
            q.pop();
        }
    }

    int pop() {
        int top = q.front();
        q.pop();
        return top;
    }

    int top() {
        return q.front();
    }

    bool empty() {
        return q.empty();
    }
};
```

---

## ⏱ Time Complexity

* `push`: O(n)
* `pop`: O(1)
* `top`: O(1)
* `empty`: O(1)

## 💾 Space Complexity

* O(n) — Space used by the queue.

---

## 🌟 Key Points

* Simulates stack behavior using queue.
* Only one queue is needed (optimized).
* Efficient for `pop`, `top`, and `empty` operations.
