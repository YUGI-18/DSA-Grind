# 🔃 Postfix to Infix Conversion

## 📝 Problem Statement

Convert a given **postfix expression** (Reverse Polish Notation) to its equivalent **infix expression**, using proper parentheses.

---

## ✨ Example

**Input:** `abc++`
**Output:** `(a + (b + c))`

**Input:** `ab*c+`
**Output:** `((a * b) + c)` ([geeksforgeeks.org][1])

---

## 🚀 Approach

1. Scan the postfix string **left to right**.
2. Push **operands** onto a stack of strings.
3. When an **operator** is encountered:

   * Pop the top two strings (`op2`, then `op1`).
   * Form `"(" + op1 + operator + op2 + ")"` and push it back.
4. Final stack item is the **fully parenthesized infix** expression.

---

## ⚙️ Algorithm Logic

1. Initialize an empty stack `st` of strings.
2. For each character `ch` in the postfix expression:

   * If **operand**, push `string(1, ch)`.
   * If **operator**:

     * Pop `op2 = st.top(); st.pop();`
     * Pop `op1 = st.top(); st.pop();`
     * Push `"(" + op1 + ch + op2 + ")"`.
3. Return `st.top()`.

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

string postfixToInfix(const string &post) {
    stack<string> st;
    for(char ch : post) {
        if(!isOperator(ch)) {
            st.push(string(1, ch));
        } else {
            string op2 = st.top(); st.pop();
            string op1 = st.top(); st.pop();
            st.push("(" + op1 + ch + op2 + ")");
        }
    }
    return st.top();
}

int main() {
    string post;
    cout << "Enter postfix expression: ";
    cin >> post;
    cout << "Infix expression: " << postfixToInfix(post) << endl;
    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** — Each character is processed once ([geeksforgeeks.org][2], [geeksforgeeks.org][1], [geeksforgeeks.org][3], [runestone.academy][4]).

## 💾 Space Complexity

* **O(n²)** in worst case — due to string concatenations.

---

## 🌟 Key Points

* Fully parenthesized for correctness.
* Simple stack of strings; no need to manage char vs string separately.

---

# 🔃 Postfix to Prefix Conversion

## 📝 Problem Statement

Convert a given **postfix expression** to its equivalent **prefix expression** using a stack.

---

## ✨ Example

**Input:** `AB+CD-*`
**Output:** `*+AB-CD` ([youtube.com][5])

---

## 🚀 Approach

1. Scan the postfix string **left to right**.
2. Push **operands** onto a stack of strings.
3. When an **operator** is found:

   * Pop top two strings: `op2`, then `op1`.
   * Form `operator + op1 + op2` and push back.
4. Final stack item is the **prefix** form.

---

## ⚙️ Algorithm Logic

1. Initialize an empty stack `st` of strings.
2. For each character `ch` in postfix:

   * If **operand**, push `string(1, ch)`.
   * If **operator**:

     * Pop `op2 = st.top(); st.pop();`
     * Pop `op1 = st.top(); st.pop();`
     * Push `ch + op1 + op2`.
3. Return `st.top()`.

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

string postfixToPrefix(const string &post) {
    stack<string> st;
    for(char ch : post) {
        if(!isOperator(ch)) {
            st.push(string(1, ch));
        } else {
            string op2 = st.top(); st.pop();
            string op1 = st.top(); st.pop();
            st.push(ch + op1 + op2);
        }
    }
    return st.top();
}

int main() {
    string post;
    cout << "Enter postfix expression: ";
    cin >> post;
    cout << "Prefix expression: " << postfixToPrefix(post) << endl;
    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** for scans; concatenation leads to **O(n²)** overall ([geeksforgeeks.org][3], [youtube.com][6], [stackoverflow.com][7]).

## 💾 Space Complexity

* **O(n)** stack + **O(n²)** string usage.

---

## 🌟 Key Points

* Efficient direct conversion, no intermediate notation.
* Stack of strings, simple concatenation logic.
* Output is the compact prefix form (no parentheses).

---
