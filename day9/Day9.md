# Day 9: 代码随想录算法训练营

## Topic:
- Stack
- Queue

## Summary
![image](https://github.com/kkkkevx/DSA/assets/108632304/7c7a5ff7-b18c-4b33-a426-ba6ae3ffd0d7)

- 

## Leetcode Problem

**[Recourse](https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html#%E6%80%9D%E8%B7%AF)**

Leetcode Porblem 232 用栈实现队列

```java
class MyQueue {
    Stack<Integer> stackIn;
    Stack<Integer> stackOut;


    public MyQueue() {
        stackIn = new Stack<>();
        stackOut = new Stack<>();
    }
    
    public void push(int x) {
        stackIn.push(x);
    }
    
    public int pop() {
        dumpIn();
        return stackOut.pop();
    }
    
    public int peek() {
        dumpIn();
        return stackOut.peek();
    }
    
    public boolean empty() {
        return stackIn.empty() && stackOut.empty();
    }

    private void dumpIn() {
        if (!stackOut.empty()) return;
        while (!stackIn.empty()) {
            stackOut.push(stackIn.pop());
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

Leetcode Problem 225 用队列实现栈

```java

class MyStack {
    Deque<Integer> que;
    public MyStack() {
        que = new ArrayDeque<>();
    }
    
    public void push(int x) {
        que.addLast(x);
    }
    
    public int pop() {
        rotate();
        return que.removeFirst();
    }
    
    public int top() {
        rotate();
        int res = que.removeFirst();
        push(res);
        return res;
    }
    
    public boolean empty() {
        return que.isEmpty();
    }
    private void rotate() {
        int size = que.size();
        while (size-- > 1) {
            push(que.removeFirst());
        }
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
