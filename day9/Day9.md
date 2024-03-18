# Day 9: 代码随想录算法训练营

## Topic:
- Stack
- Queue

## Summary
![image](https://github.com/kkkkevx/DSA/assets/108632304/7c7a5ff7-b18c-4b33-a426-ba6ae3ffd0d7)

- 双栈实现队列
  - 使用两个栈，一个用于入队操作（称为入栈），另一个用于出队操作（称为出栈）。
  - 当执行出队操作时，如果出栈为空，则将入栈中的所有元素依次弹出并压入出栈，这样可以保证最先进入入栈的元素位于出栈的栈顶，符合队列的先进先出（FIFO）特性。然后从出栈弹出元素作为出队操作的结果。
- 单队列实现栈
  - 入栈（push）操作时，先记录当前队列的长度（即栈的深度），将新元素入队，然后将队列前面的元素依次出队并重新入队直到新入队的元素移动到队列的前端，这样新入队的元素就模拟了栈顶的行为。


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
