# Stack Implementation Using Queue (C++)

## 📌 Introduction

A **Stack** follows the **LIFO (Last In First Out)** principle.

## Operations:
- **push(x)** → Insert element at top  
- **pop()** → Remove top element  
- **top()** → Return top element  
- **isEmpty()** → Check if stack is empty  

A stack can be implemented using:
1. Two Queues  
2. One Queue  

---

# ✅ Method 1: Using Two Queues

## 📌 Idea

- Maintain two queues: `q1` and `q2`
- Make `push()` costly
- Keep newest element always at the front of `q1`

---

## 📌 Algorithm

### push(x)

1. Enqueue `x` into `q2`
2. Move all elements from `q1` to `q2`
3. Swap `q1` and `q2`

### pop()

1. Dequeue from `q1`

### top()

1. Return `q1.front()`

---

## 📌 C++ Implementation (Using Two Queues)

```cpp
#include <iostream>
#include <queue>
using namespace std;

class Stack {
    queue<int> q1, q2;

public:
    void push(int x) {
        q2.push(x);

        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }

        swap(q1, q2);
        cout << x << " pushed into stack\n";
    }

    void pop() {
        if (q1.empty()) {
            cout << "Stack Underflow\n";
            return;
        }

        cout << q1.front() << " popped from stack\n";
        q1.pop();
    }

    void top() {
        if (q1.empty()) {
            cout << "Stack is Empty\n";
            return;
        }

        cout << "Top element: " << q1.front() << endl;
    }

    bool isEmpty() {
        return q1.empty();
    }
};

int main() {
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);

    s.top();

    s.pop();
    s.top();

    return 0;
}

```

## 📌 Time Complexity (Two Queues)

| Operation | Time Complexity |
| --------- | --------------- |
| push      | O(n)            |
| pop       | O(1)            |
| top       | O(1)            |

## ✅ Method 2: Using One Queue
📌 Idea

Use only one queue

After pushing, rotate the queue so the new element comes to front

## 📌 Algorithm
push(x)

Enqueue x

Rotate previous elements
(for i = 0 to size-1 → dequeue and enqueue)

## 📌 C++ Implementation (Using One Queue)
```
#include <iostream>
#include <queue>
using namespace std;

class Stack {
    queue<int> q;

public:
    void push(int x) {
        int size = q.size();
        q.push(x);

        for (int i = 0; i < size; i++) {
            q.push(q.front());
            q.pop();
        }

        cout << x << " pushed into stack\n";
    }

    void pop() {
        if (q.empty()) {
            cout << "Stack Underflow\n";
            return;
        }

        cout << q.front() << " popped from stack\n";
        q.pop();
    }

    void top() {
        if (q.empty()) {
            cout << "Stack is Empty\n";
            return;
        }

        cout << "Top element: " << q.front() << endl;
    }

    bool isEmpty() {
        return q.empty();
    }
};
```

## 📌 Time Complexity (One Queue)
| Operation | Time Complexity |
| --------- | --------------- |
| push      | O(n)            |
| pop       | O(1)            |
| top       | O(1)            |

## 📌 Key Insight

To convert FIFO → LIFO, we rearrange elements after insertion so that the newest element comes to the front.
