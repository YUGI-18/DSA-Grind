# 🔃 Prefix to Infix Conversion

## 📝 Problem Statement

Convert a given **prefix expression** (Polish notation) to its equivalent **infix expression** using a stack.

---

## ✨ Example

### Example:

**Input:** `*+AB-CD`
**Output:** `((A+B)*(C‑D))` ([geeksforgeeks.org][1])

---

## 🚀 Approach

1. **Read the prefix string** from **right to left**.
2. **Push operands** onto a stack of strings.
3. **When encountering an operator**:

   * Pop the top two operands (let’s call them `op1`, then `op2`).
   * Form a string: `"(" + op1 + operator + op2 + ")"`.
   * Push that back onto the stack.
4. At the end, the stack will contain a single string → the resulting **fully-parenthesized infix**.

---

## ⚙️ Algorithm Logic

1. Initialize an empty stack `st` of strings.
2. For each character `ch` in the prefix expression from end to start:

   * If `ch` is an **operand**, push `string(1, ch)` onto `st`.
   * If `ch` is an **operator**:

     * Pop `op1 = st.top(); st.pop();`
     * Pop `op2 = st.top(); st.pop();`
     * Push `"(" + op1 + ch + op2 + ")"` onto `st`.
3. The final element of `st` is the **infix expression**.

---

## 🔢 Code Implementation

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

bool isOperator(char x) {
    return x=='+'||x=='-'||x=='*'||x=='/'||x=='^';
}

string prefixToInfix(const string &pre) {
    stack<string> st;
    for(int i = pre.length() - 1; i >= 0; --i) {
        char ch = pre[i];
        if(isOperator(ch)) {
            string op1 = st.top(); st.pop();
            string op2 = st.top(); st.pop();
            string s = "(" + op1 + ch + op2 + ")";
            st.push(s);
        } else {
            st.push(string(1, ch));
        }
    }
    return st.top();
}

int main() {
    string prefix;
    cout << "Enter prefix expression: ";
    cin >> prefix;

    cout << "Infix expression: " << prefixToInfix(prefix) << endl;
    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** — Each symbol is processed once.

## 💾 Space Complexity

* **O(n²)** — In the worst case, concatenating strings repeatedly can consume quadratic space/time.

---

## 🌟 Key Points

* Reads from **right to left**.
* Leveraging stack of **strings**, not chars.
* Produces **fully parenthesized** infix for clarity.

---

# 🔃 Prefix to Postfix Conversion

## 📝 Problem Statement

Convert a given **prefix expression** to **postfix notation** using a stack.

---

## ✨ Example

### Example:

**Input:** `*+AB-CD`
**Output:** `AB+CD-*` ([prepbytes.com][2], [geeksforgeeks.org][1], [en.wikipedia.org][3], [stackoverflow.com][4], [stackoverflow.com][5], [en.wikipedia.org][6])

---

## 🚀 Approach

1. **Read the prefix string** from **right to left**.
2. **Push operands** onto a string stack.
3. **On encountering an operator**:

   * Pop `op1` and `op2` from the stack.
   * Form a string: `op1 + op2 + operator`.
   * Push that back onto the stack.
4. At the end, the stack’s single string is the **postfix** expression.

---

## ⚙️ Algorithm Logic

1. Initialize an empty stack `st` of strings.
2. For each character `ch` in the prefix input, processed from end to start:

   * If **operand** → push as string onto `st`.
   * If **operator**:

     * Pop `op1 = st.top(); st.pop();`
     * Pop `op2 = st.top(); st.pop();`
     * Push `(op1 + op2 + ch)` onto `st`.
3. Output `st.top()` as the resulting **postfix** form.

---

## 🔢 Code Implementation

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

bool isOperator(char x) {
    return x=='+'||x=='-'||x=='*'||x=='/'||x=='^';
}

string prefixToPostfix(const string &pre) {
    stack<string> st;
    for(int i = pre.length() - 1; i >= 0; --i) {
        char ch = pre[i];
        if(isOperator(ch)) {
            string op1 = st.top(); st.pop();
            string op2 = st.top(); st.pop();
            string s = op1 + op2 + ch;
            st.push(s);
        } else {
            st.push(string(1, ch));
        }
    }
    return st.top();
}

int main() {
    string prefix;
    cout << "Enter prefix expression: ";
    cin >> prefix;

    cout << "Postfix expression: " << prefixToPostfix(prefix) << endl;
    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** per character; but string concatenation might introduce additional cost → **O(n²)** in total .

## 💾 Space Complexity

* **O(n)** for the stack and **O(n²)** for building strings.

---

## 🌟 Key Points

* Efficiently converts **directly** from prefix to postfix.
* Stack-based, simple string operations.
* Eliminates parentheses for neat postfix output.

---
