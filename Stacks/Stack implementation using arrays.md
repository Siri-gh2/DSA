# Stack Implementation Using Array in C++

This document demonstrates a basic **Stack Data Structure** implementation using an **array**.
The stack follows the **LIFO (Last In, First Out)** principle.

---

## 📌 Features Implemented

- Push (Insert element)
- Pop (Remove element)
- Peek (View top element)
- Check if stack is empty
- Check if stack is full
- Display stack elements
- Proper memory management using constructor & destructor

---

## 📥 Input

- Size of the stack (integer)

---

## 📤 Output

- Stack elements after push and pop operations
- Top element of the stack
- Error messages for overflow and underflow conditions

---

## 🧠 Stack Operations Explanation

| Operation | Description |
|---------|-------------|
| `push(x)` | Inserts element `x` into the stack |
| `pop()` | Removes and returns the top element |
| `peek()` | Returns the top element without removing it |
| `isEmpty()` | Checks if the stack is empty |
| `isFull()` | Checks if the stack is full |
| `display()` | Displays all elements of the stack |

---

## 💻 C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

class Stack {
    int* arr;
    int capacity;
    int top;

public:
    Stack(int cap) {
        capacity = cap;
        arr = new int[capacity];
        top = -1;
    }

    ~Stack() {
        delete[] arr;
    }

    // Push operation
    void push(int x) {
        if (top == capacity - 1) {
            cout << "Stack overflow" << endl;
            return;
        }
        arr[++top] = x;
    }

    // Pop operation
    int pop() {
        if (top == -1) {
            cout << "Stack underflow" << endl;
            return -1;
        }
        return arr[top--];
    }

    // Peek operation
    int peek() {
        if (top == -1) {
            cout << "Stack is empty" << endl;
            return -1;
        }
        return arr[top];
    }

    // Check if stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Check if stack is full
    bool isFull() {
        return top == capacity - 1;
    }

    // Display stack elements
    void display() {
        if (isEmpty()) {
            cout << "Stack is empty" << endl;
            return;
        }
        for (int i = 0; i <= top; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    int size;
    cout << "Size of stack: ";
    cin >> size;

    Stack s(size);

    s.push(1);
    s.push(2);
    s.push(3);

    s.display();

    s.pop();
    s.display();

    cout << "Top element: " << s.peek() << endl;

    return 0;
}

Time Complexity

| Operation | Complexity |
| --------- | ---------- |
| Push      | O(1)       |
| Pop       | O(1)       |
| Peek      | O(1)       |
| Display   | O(n)       |

**📌 Notes**
This stack implementation uses dynamic memory allocation

Handles overflow and underflow conditions

Suitable for understanding core stack concepts before STL usage


