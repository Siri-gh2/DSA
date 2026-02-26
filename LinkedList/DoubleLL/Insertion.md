# Doubly Linked List – Insertion

Insertion can be done in three ways:
- At Beginning
- At End
- At Position

---

## 💻 C++ Program: Insertion Cases

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

    // Insert at Beginning
    void insertAtBeginning(int x) {
        Node* newNode = new Node(x);

        if (head == nullptr) {
            head = newNode;
            return;
        }

        newNode->next = head;
        head->prev = newNode;
        head = newNode;
    }

    // Insert at End
    void insertAtEnd(int x) {
        Node* newNode = new Node(x);

        if (head == nullptr) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }

        temp->next = newNode;
        newNode->prev = temp;
    }

    // Insert at Position (1-based)
    void insertAtPosition(int x, int pos) {
        if (pos == 1) {
            insertAtBeginning(x);
            return;
        }

        Node* newNode = new Node(x);
        Node* temp = head;

        for (int i = 1; temp != nullptr && i < pos - 1; i++) {
            temp = temp->next;
        }

        if (temp == nullptr) return;

        newNode->next = temp->next;
        newNode->prev = temp;

        if (temp->next != nullptr)
            temp->next->prev = newNode;

        temp->next = newNode;
    }
};
```
## Complexity :

- Beginning: O(1)
- End: O(n)
- Position: O(n)
