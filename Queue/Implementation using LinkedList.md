# Queue Implementation Using Linked List (C++)

## 📌 Introduction

A **Queue** follows the **FIFO (First In First Out)** principle.

In a Linked List implementation:
- Each element is stored in a **node**
- Each node contains:
  - `data`
  - `next` pointer
- We maintain two pointers:
  - `front`
  - `rear`

---

## 📌 Why Use Linked List for Queue?

✅ No fixed size limitation  
✅ No memory wastage  
✅ Dynamic memory allocation  
✅ Efficient O(1) insertion and deletion  

---

## 📌 Structure of Node

```cpp
struct Node {
    int data;
    Node* next;
};
```

## 📌 Algorithm
# Enqueue(x)
```
Create a new node.

- If queue is empty:

    - front = rear = newNode

- Else:

   - rear->next = newNode

    - rear = newNode
```
## Dequeue()
```
- If queue is empty → Underflow

- Else:

   1.Store front in temp

   2.front = front->next

   3.Delete temp

- If front == NULL

- rear = NULL

```
## C++ Implementation
```
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

class Queue {
    Node* front;
    Node* rear;

public:
    Queue() {
        front = rear = NULL;
    }

    void enqueue(int x) {
        Node* newNode = new Node();
        newNode->data = x;
        newNode->next = NULL;

        if (rear == NULL) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }

        cout << x << " inserted into queue\n";
    }

    void dequeue() {
        if (front == NULL) {
            cout << "Queue Underflow\n";
            return;
        }

        Node* temp = front;
        cout << front->data << " removed from queue\n";
        front = front->next;

        if (front == NULL)
            rear = NULL;

        delete temp;
    }

    void peek() {
        if (front == NULL) {
            cout << "Queue is Empty\n";
            return;
        }

        cout << "Front element: " << front->data << endl;
    }

    bool isEmpty() {
        return (front == NULL);
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.peek();

    q.dequeue();
    q.peek();

    return 0;
}
```

## Time Complexity

| Operation | Time Complexity |
| --------- | --------------- |
| Enqueue   | O(1)            |
| Dequeue   | O(1)            |
| Peek      | O(1)            |

## Advantages Over Array Implementation

- No fixed size limit

- No wasted memory

- Efficient dynamic growth

