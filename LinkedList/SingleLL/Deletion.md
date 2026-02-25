
---

# linked_list_deletion.md`

```md
# Singly Linked List – Deletion Operations

Deletion removes a node from the linked list safely.

---

## 📌 Types of Deletion
1. From Beginning
2. From End
3. From Specific Position

---

## 💻 C++ Program: Deletion & Display

```cpp
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int x) {
        data = x;
        next = nullptr;
    }
};

class LinkedList {
    Node* head;

public:
    LinkedList() {
        head = nullptr;
    }

    void insertAtEnd(int x) {
        Node* newNode = new Node(x);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next)
            temp = temp->next;
        temp->next = newNode;
    }

    // Delete from beginning
    void deleteFromBeginning() {
        if (!head) {
            cout << "List is empty" << endl;
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    // Delete from end
    void deleteFromEnd() {
        if (!head) {
            cout << "List is empty" << endl;
            return;
        }

        if (!head->next) {
            delete head;
            head = nullptr;
            return;
        }

        Node* temp = head;
        while (temp->next->next)
            temp = temp->next;

        delete temp->next;
        temp->next = nullptr;
    }

    // Delete at position (1-based)
    void deleteAtPosition(int pos) {
        if (pos == 1) {
            deleteFromBeginning();
            return;
        }

        Node* temp = head;
        for (int i = 1; i < pos - 1 && temp != nullptr; i++)
            temp = temp->next;

        if (!temp || !temp->next) {
            cout << "Invalid position" << endl;
            return;
        }

        Node* del = temp->next;
        temp->next = del->next;
        delete del;
    }

    void display() {
        Node* temp = head;
        while (temp) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }
};

int main() {
    LinkedList list;

    list.insertAtEnd(10);
    list.insertAtEnd(20);
    list.insertAtEnd(30);
    list.insertAtEnd(40);

    list.deleteFromBeginning();
    list.deleteAtPosition(2);
    list.deleteFromEnd();

    list.display();

    return 0;
}

output:
20 -> NULL

Complexity

| Operation        | Time |
| ---------------- | ---- |
| Delete Beginning | O(1) |
| Delete End       | O(n) |
| Delete Position  | O(n) |



