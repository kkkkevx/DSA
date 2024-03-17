# Day 9: 代码随想录算法训练营

## Topic:
- Stack

## Summary
- LIFO (Last In, First Out)
- Reverse Polish Notation (RPN): The current code implementation has a potential logical error when dealing with "-" and "/" operations, as it assumes that the second popped element is the left operand of the operator, and the first popped element is the right operand. This may lead to incorrect calculation results.
- In the Deque class, the main point to note is the value of the head pointer on push and offer operations (also pull and poll). In the case of push, the head will point to the newly pushed element, but in offer, the head will still point to the first inserted element.

## Leetcode Problem

**[Recourse](https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)**

Leetcode Problem 20 有效的括号

```java
class Solution {
    public boolean isValid(String s) {

        //Main point here is what is head value on push & offer (also pull & poll), incase of push head will be pointing to newly pushed element but in offer head will still be pointing to first inserted element.
        Deque<Character> deque = new LinkedList<>();
        char ch;
        for (int i = 0; i < s.length(); i++) {
            ch = s.charAt(i);
            if (ch == '(') {
                deque.push(')');
            }else if (ch == '{') {
                deque.push('}');
            }else if (ch == '[') {
                deque.push(']');
            } else if (deque.isEmpty() || deque.peek() != ch) {
                return false;
            }else {
                deque.pop();
            }
        }
        return deque.isEmpty();
    }
}
```

Leetcode Problem 1047 删除字符串中的所有相邻重复项
```java
class Solution {
    public String removeDuplicates(String s) {
        Deque<Character> deque = new ArrayDeque<>();
        StringBuilder str = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (deque.isEmpty() || deque.peek() != s.charAt(i)) {
                deque.push(s.charAt(i));
            } else {
                deque.pop();
            }
        }

        while (!deque.isEmpty()) {
            str.append(deque.pop());
        }

        return str.reverse().toString();

    }
}
```

Leetcode Problem 150 逆波兰表达式求值
```java
class Solution {
    public int evalRPN(String[] tokens) {
        // 当前的代码实现在处理 - 和 / 时有一个潜在的逻辑错误，因为它假设了第二次弹出的元素是操作符的左操作数，而第一次弹出的元素是右操作数。这可能导致计算结果不正确。
        Deque<Integer> deque = new ArrayDeque<>();

        for (int i = 0; i < tokens.length; i++) {
            if (tokens[i].equals("+")) {
                deque.push(deque.pop() + deque.pop());
            } else if (tokens[i].equals("-")) {
                int num1 = deque.pop();
                int num2 = deque.pop();
                deque.push(num2 - num1);
            } else if (tokens[i].equals("*")) {
                deque.push(deque.pop() * deque.pop());
            } else if (tokens[i].equals("/")) {
                int num1 = deque.pop();
                int num2 = deque.pop();
                deque.push(num2 / num1);
            } else {
                deque.push(Integer.parseInt(tokens[i]));
            }
        }

        return deque.pop();
    }
}
```


  
