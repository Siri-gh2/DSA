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
//push
    void push(int x) {
        if (top == capacity - 1) {
            cout << "Stack overflow" << endl;
            return;
        }
        arr[++top] = x;
    }
//pop
    int pop() {
        if (top == -1) {
            cout << "Stack underflow" << endl;
            return -1;
        }
        return arr[top--];
    }
//peekvalue
    int peek() {
        if (top == -1) {
            cout << "Stack is empty" << endl;
            return -1;
        }
        return arr[top];
    }
//empty stack
    bool isEmpty() {
        return top == -1;
    }
//stack is full
    bool isFull() {
        return top == capacity - 1;
    }
//display stack
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
