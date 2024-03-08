#Day 3: 代码随想录算法训练营

## Topic:
- Linked List


## Summary:
- 基础的linked list
- 考验写基本代码的基础和细节
- 在写链表增删的时候 会忘记验证输入值（size < 0）
- 在用dummy的时候，对于指针指向谁要多加体会
- 这三道题都不难 都能AC， 但是还是会花很多时间去debug一些小错误
- 问题还是 看到问题就想狂飙代码 没有逻辑验证。 

## Leetcode 203. 移除链表元素：
**[Problem](https://leetcode.cn/problems/remove-linked-list-elements/description/)**

**[Recourse](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)**

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1, head);
        ListNode pre = dummy;
        ListNode cur = head;

        while (cur != null) {
            if (cur.val == val) {
                pre.next = pre.next.next;
            } else {
                pre = cur;
            }
            cur = cur.next;
        }

        return dummy.next;
    }
}
```

## 707. 设计链表：
**[Problem](https://leetcode.cn/problems/design-linked-list/description/)**

**[Recourse](https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html)**

``` java
class MyLinkedList {
    class Node{
        int val;
        Node next;
        public Node(){};

        public Node(int val) {
            this.val = val;
        }

        public Node(int val, Node next) {
            this.val = val;
            this.next = next;
        }
    }
    Node dummyHead;
    int size;
    public MyLinkedList() {
        size = 0;
        dummyHead = new Node(0);
    }
    
    public int get(int index) {
        if (index < 0 || index >= size) return -1;

        Node cur = dummyHead;
        for (; index >= 0; index--) {
            cur = cur.next;
        }
        return cur.val;
    }
    
    public void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    public void addAtTail(int val) {
        addAtIndex(size, val);
    }
    
    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) return;
        size++;
        Node pre = dummyHead;
        for(int i = 0; i < index; i++) {
            pre = pre.next;
        }
        
        Node newNode = new Node(val);
        newNode.next = pre.next;
        pre.next = newNode;
    }
    
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) return;

        size--;
        Node pre = dummyHead;
        for (int i = 0; i < index; i++) {
            pre = pre.next;
        }

        pre.next = pre.next.next;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```


## Leetcode 206. 反转链表：
**[Problem](https://leetcode.cn/problems/reverse-linked-list/description/)**

**[Recourse](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html)**

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode temp = null;
        ListNode cur = head;

        while (cur != null) {
            temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }

        return pre;
    }
}

```