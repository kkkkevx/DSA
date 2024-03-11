# Day 3: 代码随想录算法训练营

## Topic:
- Linked List
- slow and fast pointer
- 环形指针


## Summary:
- 在链表，有哨兵节点会简单很多
- 不要忘记继续移动指针这个小细节
- 环形指针： 从头结点出发一个指针，从相遇节点 也出发一个指针，这两个指针每次只走一个节点， 那么当这两个指针相遇的时候就是 环形入口的节点。 x + y = n(y + z) when n = 1, x = z
- 对于删除倒数节点， 一定要多走一步是因为fast要走到null 才会停下
- 这次刷题比第一次自己刷理解更加快速
- 希望以后能自己AC

## Leetcode 24. 两两交换链表中的节点：
**[Problem](https://leetcode.cn/problems/swap-nodes-in-pairs/description/)**

**[Recourse](https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html)** 

``` Java
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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1, head);
        ListNode cur = dummy;

        while (cur.next != null && cur.next.next != null) {
            ListNode tmp  = cur.next;
            ListNode tmp1 = cur.next.next.next;

            cur.next = cur.next.next;
            cur.next.next = tmp;
            cur.next.next.next = tmp1;

            cur = cur.next.next;
        }

        return dummy.next;
    }
}
```

## Leetcode 面试题 02.07. 链表相交：
**[Problem](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/description/)**

**[Recourse](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF)** 

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lengthA = 0, lengthB = 0;
        ListNode curA = headA, curB = headB;
        while (curA != null) {
            lengthA++;
            curA = curA.next;
        }

        while (curB != null) {
            lengthB++;
            curB = curB.next;
        }
        
        int gap = lengthA - lengthB;
        if (gap < 0) {
            curA = headB;
            curB = headA;
            gap *= -1;
        } else {
            curA = headA;
            curB = headB;
        }

        for (int i = 0; i < gap; i++) {
            curA = curA.next;
        }

        while (curB != null) {
            if (curA == curB) {
                return curA;
            }
            curA = curA.next;
            curB = curB.next;
        }

        return null;
    }
}
```

## Leetcode 19. 删除链表的倒数第 N 个结点：
**[Problem](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/description/)**

**[Recourse](https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html)** 

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(-1, head);
        ListNode fast = dummy, slow = dummy;

        //这里为什么要走n+1一步 因为fast要到null才会停下来 所以要多一步
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }

        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;

        return dummy.next;
    }
}
```

## Leetcode 142. 环形链表 II：
**[Problem](https://leetcode.cn/problems/linked-list-cycle-ii/description/)**

**[Recourse](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF)** 

``` java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head, fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next; 
            fast = fast.next.next;
            if (slow == fast) {
                ListNode index1 = head, index2 = slow;

                // x + y = n (y + z)  when n = 1, x = z 
                while (index1 != index2) {
                    index1 = index1.next;
                    index2 = index2.next;
                }

                return index1;
            }
        }

        return null;
    }
}

```
