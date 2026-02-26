# Doubly Linked List – Deletion

Deletion can be done in three ways:
- From Beginning
- From End
- From Position

---

## 💻 C++ Program: Deletion Cases

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;

    Node(int x) {
        data = x;
        prev = nullptr;
        next = nullptr;
    }
};

class DoublyLinkedList {
    Node* head;

public:
    DoublyLinkedList() {
        head = nullptr;
    }

    // Delete from Beginning
    void deleteFromBeginning() {
        if (head == nullptr) return;

        Node* temp = head;
        head = head->next;

        if (head != nullptr)
            head->prev = nullptr;

        delete temp;
    }

    // Delete from End
    void deleteFromEnd() {
        if (head == nullptr) return;

        Node* temp = head;

        while (temp->next != nullptr)
            temp = temp->next;

        if (temp->prev != nullptr)
            temp->prev->next = nullptr;
        else
            head = nullptr;

        delete temp;
    }

    // Delete at Position (1-based)
    void deleteAtPosition(int pos) {
        if (head == nullptr) return;

        if (pos == 1) {
            deleteFromBeginning();
            return;
        }

        Node* temp = head;

        for (int i = 1; temp != nullptr && i < pos; i++) {
            temp = temp->next;
        }

        if (temp == nullptr) return;

        if (temp->next != nullptr)
            temp->next->prev = temp->prev;

        if (temp->prev != nullptr)
            temp->prev->next = temp->next;

        delete temp;
    }
};
```
## Complexity :

- Beginning: O(1)
- End: O(n)
- Position: O(n)
