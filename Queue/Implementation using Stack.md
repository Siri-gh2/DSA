# Queue Implementation Using Stack (C++)

## 📌 Introduction

A **Queue** follows the **FIFO (First In First Out)** principle.

Operations:
- **enqueue(x)** → Insert element at rear  
- **dequeue()** → Remove element from front  
- **front()** → Get front element  
- **isEmpty()** → Check if queue is empty  

A queue can be implemented using:
1. Two Stacks (Efficient Method)
2. Single Stack (Recursive Method)

---

# ✅ Method 1: Using Two Stacks (Efficient)

## 📌 Idea

- Use two stacks: `s1` and `s2`
- `s1` → Used for enqueue  
- `s2` → Used for dequeue  

When dequeuing:
- If `s2` is empty, transfer all elements from `s1` to `s2`
- This reverses order to maintain FIFO

---

## 📌 Algorithm

### Enqueue(x)

1. Push `x` into `s1`

### Dequeue()

1. If both stacks are empty → Underflow  
2. If `s2` is empty  
   - Move all elements from `s1` to `s2`
3. Pop from `s2`

---

## 📌 C++ Implementation (Two Stacks)

```cpp
#include <iostream>
#include <stack>
using namespace std;

class Queue {
    stack<int> s1, s2;

public:
    void enqueue(int x) {
        s1.push(x);
        cout << x << " inserted into queue\n";
    }

    void dequeue() {
        if (s1.empty() && s2.empty()) {
            cout << "Queue Underflow\n";
            return;
        }

        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }

        cout << s2.top() << " removed from queue\n";
        s2.pop();
    }

    void front() {
        if (s1.empty() && s2.empty()) {
            cout << "Queue is Empty\n";
            return;
        }

        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }

        cout << "Front element: " << s2.top() << endl;
    }

    bool isEmpty() {
        return (s1.empty() && s2.empty());
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.front();

    q.dequeue();
    q.front();

    return 0;
}
```

## 📌 Time Complexity (Two Stacks Method)

| Operation | Time Complexity  |
| --------- | ---------------- |
| Enqueue   | O(1)             |
| Dequeue   | O(1) (Amortized) |
| Front     | O(1) (Amortized) |

## ✅ Method 2: Using Single Stack (Recursive Method)
📌 Idea

Push element normally

During dequeue, use recursion to reach bottom element

Remove bottom element (oldest)

⚠️ This method is less efficient and uses recursion stack.

## C++ Implementation (Single Stack)
```
#include <iostream>
#include <stack>
using namespace std;

class Queue {
    stack<int> s;

public:
    void enqueue(int x) {
        s.push(x);
        cout << x << " inserted into queue\n";
    }

    int dequeueHelper() {
        if (s.empty()) {
            cout << "Queue Underflow\n";
            return -1;
        }

        int x = s.top();
        s.pop();

        if (s.empty()) {
            return x;
        }

        int item = dequeueHelper();
        s.push(x);
        return item;
    }

    void dequeue() {
        int val = dequeueHelper();
        if (val != -1)
            cout << val << " removed from queue\n";
    }
};

```
## 📌 Time Complexity (Single Stack Method)

| Operation | Time Complexity |
| --------- | --------------- |
| Enqueue   | O(1)            |
| Dequeue   | O(n)            |
| Front     | O(n)            |

📌 Key Insight

- To convert LIFO → FIFO, we reverse the order of elements using:

- Another stack (efficient method)

- Recursion (less efficient method)
