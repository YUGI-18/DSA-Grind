
#### 🐢🐇 Linked List: Fast and Slow Pointer

```cpp
int fn(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    int ans = 0;

    while (fast != nullptr && fast->next != nullptr) {
        // do logic
        slow = slow->next;
        fast = fast->next->next;
    }

    return ans;
}
```

**🔹 Use When:**

* You need to find the **middle node**, **detect cycles**, or handle problems requiring different traversal speeds.
* Common problems:

  * Find Middle of Linked List
  * Detect Cycle (Floyd’s Algorithm)
  * Check for Palindrome (with reverse half)

---

#### 🔁 Reversing a Linked List

```cpp
ListNode* fn(ListNode* head) {
    ListNode* curr = head;
    ListNode* prev = nullptr;

    while (curr != nullptr) {
        ListNode* nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }

    return prev;
}
```

**🔹 Use When:**

* You need to reverse the entire linked list (or part of it).
* Common problems:

  * Reverse Linked List
  * Reverse in k-Groups
  * Compare halves of a list
  * Undo pointer structure

**🔹 How to Use:**

* Use the returned `prev` as the new head of the reversed list.

---
