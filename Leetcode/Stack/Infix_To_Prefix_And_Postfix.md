# 🔁 Infix to Prefix Conversion

## 📝 Problem Statement

Convert a given **infix expression** to its equivalent **prefix expression** using a stack-based approach.

### Definitions:

* **Infix**: Operators are written between operands.
  Example: `(A + B)`
* **Prefix (Polish Notation)**: Operators are written before operands.
  Example: `+ A B`

---

## ✨ Example

### Example 1:

**Input:** `(A+B)*(C-D)`
**Output:** `*+AB-CD`

### Example 2:

**Input:** `A+(B*C)`
**Output:** `+A*BC`

---

## 🚀 Approach

* Convert infix to prefix by using a modified infix-to-postfix approach:

  1. Reverse the infix expression.
  2. Swap every `'('` with `')'` and vice versa.
  3. Apply **infix to postfix** logic to the modified expression.
  4. Reverse the resulting postfix to get the final prefix expression.

---

## ⚙️ Algorithm Logic

1. **Reverse** the infix string.
2. **Swap parentheses**: Replace `(` with `)` and vice versa.
3. **Use a stack** to convert the reversed expression to postfix:

   * If it's an operand → Add to result.
   * If it's `(` → Push to stack.
   * If it's `)` → Pop and append until `(` is found.
   * If it's an operator → Pop operators with higher or equal precedence and append, then push the current one.
4. **Reverse** the postfix expression → This is the final prefix.

---

## 🔢 Code Implementation

```cpp
#include <iostream>
#include <stack>
#include <algorithm>
#include <cctype>
using namespace std;

int precedence(char op) {
    if(op == '^') return 3;
    if(op == '*' || op == '/') return 2;
    if(op == '+' || op == '-') return 1;
    return -1;
}

string infixToPostfix(string s) {
    stack<char> st;
    string result;

    for(char ch : s) {
        if(isalnum(ch)) {
            result += ch;
        } else if(ch == '(') {
            st.push(ch);
        } else if(ch == ')') {
            while(!st.empty() && st.top() != '(') {
                result += st.top(); st.pop();
            }
            if(!st.empty()) st.pop(); // pop '('
        } else {
            while(!st.empty() && precedence(st.top()) >= precedence(ch)) {
                if(ch == '^' && st.top() == '^') break; // right-associative
                result += st.top(); st.pop();
            }
            st.push(ch);
        }
    }

    while(!st.empty()) {
        result += st.top(); st.pop();
    }

    return result;
}

string infixToPrefix(string s) {
    reverse(s.begin(), s.end());

    for(char& ch : s) {
        if(ch == '(') ch = ')';
        else if(ch == ')') ch = '(';
    }

    string postfix = infixToPostfix(s);
    reverse(postfix.begin(), postfix.end());

    return postfix;
}

int main() {
    string expression;
    cout << "Enter infix expression: ";
    cin >> expression;

    string prefix = infixToPrefix(expression);
    cout << "Prefix Expression: " << prefix << endl;

    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** — Each character is processed once, where *n* is the length of the input.

## 💾 Space Complexity

* **O(n)** — For the stack and result string.

---

## 🌟 Key Points

* Reverse the expression and swap brackets to simplify conversion.
* Reuse postfix logic to generate prefix.
* Stack handles precedence and associativity efficiently.

---

# 🔁 Infix to Postfix Conversion

## 📝 Problem Statement

Convert a given **infix expression** to its equivalent **postfix expression** using a stack.

### Definitions:

* **Infix**: `(A + B)`
* **Postfix (Reverse Polish Notation)**: `A B +`

---

## ✨ Example

### Example 1:

**Input:** `(A+B)*(C-D)`
**Output:** `AB+CD-*`

### Example 2:

**Input:** `A+(B*C)`
**Output:** `ABC*+`

---

## 🚀 Approach

* Use a stack to store operators and output operands directly.
* Handle parentheses by pushing `'('` and popping till `'('` on `')'`.
* While encountering an operator:

  * Pop from stack all operators with higher or equal precedence and append them to result.
  * Push the current operator to stack.
* Pop remaining operators from the stack at the end.

---

## ⚙️ Algorithm Logic

1. Initialize an empty stack and result string.
2. **Scan** the infix string from left to right:

   * If it's an operand → Add to result.
   * If it's `'('` → Push to stack.
   * If it's `')'` → Pop and append until `'('` is encountered, then pop `'('`.
   * If it's an operator:

     * Pop operators from stack to result **while precedence is higher or equal**.
     * Push the current operator onto the stack.
3. **After traversal**, pop all remaining operators from the stack to result.

---

## 🔢 Code Implementation

```cpp
#include <iostream>
#include <stack>
#include <cctype>
using namespace std;

int precedence(char op) {
    if(op == '^') return 3;
    if(op == '*' || op == '/') return 2;
    if(op == '+' || op == '-') return 1;
    return -1;
}

string infixToPostfix(string s) {
    stack<char> st;
    string result;

    for(char ch : s) {
        if(isalnum(ch)) {
            result += ch;
        } else if(ch == '(') {
            st.push(ch);
        } else if(ch == ')') {
            while(!st.empty() && st.top() != '(') {
                result += st.top(); st.pop();
            }
            if(!st.empty()) st.pop(); // remove '('
        } else {
            while(!st.empty() && precedence(st.top()) >= precedence(ch)) {
                if(ch == '^' && st.top() == '^') break; // Right associative
                result += st.top(); st.pop();
            }
            st.push(ch);
        }
    }

    while(!st.empty()) {
        result += st.top(); st.pop();
    }

    return result;
}

int main() {
    string expression;
    cout << "Enter infix expression: ";
    cin >> expression;

    string postfix = infixToPostfix(expression);
    cout << "Postfix Expression: " << postfix << endl;

    return 0;
}
```

---

## ⏱ Time Complexity

* **O(n)** — Each character is visited once.

## 💾 Space Complexity

* **O(n)** — Stack and result string require extra space.

---

## 🌟 Key Points

* Postfix expressions eliminate the need for parentheses.
* Stack ensures proper handling of operator precedence and associativity.
* Widely used in compilers and expression evaluation.

---
