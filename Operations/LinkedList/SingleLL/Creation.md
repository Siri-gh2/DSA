# Singly Linked List – Creation

A **Singly Linked List** is a linear data structure where each node contains:
- `data`
- a pointer to the `next` node

The list starts with a pointer called **head**.

---

## 🧠 Node Structure

```cpp
class Node {
public:
    int data;
    Node* next;

    Node(int x) {
        data = x;
        next = nullptr;
    }
};
```
💻 C++ Program: Creation & Display
```
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

    // Create list by inserting at end
    void create(int x) {
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
    }

    // Display list
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

    list.create(10);
    list.create(20);
    list.create(30);

    list.display();

    return 0;
}

```
Example Output
10 -> 20 -> 30 -> NULL

⏱** Complexity**
Creation (end): O(n)

Display: O(n)


