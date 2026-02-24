# Queue Implementation Using Array (C++)

## 📌 Introduction

A **Queue** is a linear data structure that follows the **FIFO (First In First Out)** principle.

- Insertion happens at the **rear**
- Deletion happens from the **front**

---

## 📌 Queue Operations

1. **Enqueue(x)** – Insert element at the rear  
2. **Dequeue()** – Remove element from the front  
3. **Peek()** – Get the front element  
4. **isEmpty()** – Check if queue is empty  
5. **isFull()** – Check if queue is full  

---

## 📌 Algorithm

### Enqueue(x)
```
1. If `rear == size - 1` → Queue Overflow  
2. Else  
   - If `front == -1` → `front = 0`  
   - `rear = rear + 1`  
   - `arr[rear] = x`  
```
### Dequeue()
```
1. If `front == -1` OR `front > rear` → Queue Underflow  
2. Else  
   - Print `arr[front]`  
   - `front = front + 1`  
```
---

## 📌 C++ Implementation

```cpp
#include <iostream>
using namespace std;

class Queue {
    int *arr;
    int front;
    int rear;
    int size;

public:
    Queue(int s) {
        size = s;
        arr = new int[size];
        front = -1;
        rear = -1;
    }

    void enqueue(int x) {
        if (rear == size - 1) {
            cout << "Queue Overflow\n";
            return;
        }

        if (front == -1)
            front = 0;

        rear++;
        arr[rear] = x;
        cout << x << " inserted into queue\n";
    }

    void dequeue() {
        if (front == -1 || front > rear) {
            cout << "Queue Underflow\n";
            return;
        }

        cout << arr[front] << " removed from queue\n";
        front++;
    }

    void peek() {
        if (front == -1 || front > rear) {
            cout << "Queue is Empty\n";
            return;
        }
        cout << "Front element: " << arr[front] << endl;
    }

    bool isEmpty() {
        return (front == -1 || front > rear);
    }
};

int main() {
    Queue q(5);

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.peek();

    q.dequeue();
    q.peek();

    return 0;
}

```
## TIME COMPLEXITY

| Operation | Time Complexity |
| --------- | --------------- |
| Enqueue   | O(1)            |
| Dequeue   | O(1)            |
| Peek      | O(1)            |


## Limitation of Simple Queue Using Array

- After several dequeue operations, empty space at the beginning cannot be reused.

- Leads to memory wastage.

- Solution: Circular Queue
