
---

# linked_list_insertion

```md
# Singly Linked List – Insertion Operations

Insertion means adding a new node to the linked list.

---

## 📌 Types of Insertion
1. At Beginning
2. At End
3. At Specific Position

---

## 💻 C++ Program: Insertion & Display

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

    // Insert at beginning
    void insertAtBeginning(int x) {
        Node* newNode = new Node(x);
        newNode->next = head;
        head = newNode;
    }

    // Insert at end
    void insertAtEnd(int x) {
        Node* newNode = new Node(x);

        if (head == nullptr) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr)
            temp = temp->next;

        temp->next = newNode;
    }

    // Insert at position (1-based)
    void insertAtPosition(int x, int pos) {
        if (pos == 1) {
            insertAtBeginning(x);
            return;
        }

        Node* temp = head;
        for (int i = 1; i < pos - 1 && temp != nullptr; i++)
            temp = temp->next;

        if (temp == nullptr) {
            cout << "Invalid position" << endl;
            return;
        }

        Node* newNode = new Node(x);
        newNode->next = temp->next;
        temp->next = newNode;
    }

    void display() {
        Node* temp = head;
        while (temp != nullptr) {
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

    list.insertAtBeginning(5);
    list.insertAtPosition(15, 3);

    list.display();

    return 0;
}
Example Output
5 -> 10 -> 15 -> 20 -> NULL

⏱ Complexity

| Operation           | Time |
| ------------------- | ---- |
| Insert at Beginning | O(1) |
| Insert at End       | O(n) |
| Insert at Position  | O(n) |



