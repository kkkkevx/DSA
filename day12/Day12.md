# Day 12: 代码随想录算法训练营

## Topic:
- Binary Tree
- BFS:
  - recursive: pre-order, inorder, post-order
  - stack

## Summary:
- 递归：
  - **确定递归函数的参数和返回值：** 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。
  - **确定终止条件：** 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。
  - **确定单层递归的逻辑：** 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。
- Recursive BFS is easy to understand follower the rule of order
- stack BFS:
**1. 前序遍历 (Pre-order Traversal)
**前序遍历的顺序是根节点 -> 左子树 -> 右子树。

算法步骤
创建一个空栈，将根节点压入栈中。
当栈不为空时，循环执行以下步骤：
弹出一个节点，访问它。
将其右子节点（如果有）压入栈中。
将其左子节点（如果有）压入栈中。（因为栈是后进先出的数据结构，我们希望先处理左子节点）

**2. 中序遍历 (In-order Traversal)
**中序遍历的顺序是左子树 -> 根节点 -> 右子树。

算法步骤
创建一个空栈，当前节点设置为根节点。
当当前节点不为空或栈不为空时，循环执行以下步骤：
将当前节点及其所有左子节点压入栈中，然后设置当前节点为其左子节点。
当当前节点为空且栈不为空时，弹出栈顶元素，访问它，并将当前节点设置为弹出节点的右子节点。

**3. 后序遍历 (Post-order Traversal)**
按照preorder 换左右子节点的顺序 最后reverse 从出栈顺序 中右左 反转成 左右中完成 后序遍历

## Leetcode Problem

[Recourse](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)

Leetcode problem 144(pre)， 94(in)， 145(post)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        preOrderStack(root, res);
        return res;
    }

    private void preOrderRecursive(TreeNode root, List res) {
        if (root == null) return;

        res.add(root.val);
        preOrderRecursive(root.left, res);
        preOrderRecursive(root.right, res);
    }

    private void preOrderStack(TreeNode root, List res) {
        if (root == null) return;

        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            res.add(cur.val);

            if (cur.right != null) {
                stack.push(cur.right);
            }

            if (cur.left != null) {
                stack.push(cur.left);
            }
        }
    }
}
```


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inOrderRecursive(root, res);
        return res;
    }
    private void inOrderRecursive(TreeNode root, List res) {
        if (root == null) return;

        inOrderRecursive(root.left, res);
        res.add(root.val);
        inOrderRecursive(root.right, res);
    }

    private void inOrderStack(TreeNode root, List res) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode cur = root;

        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.pop();
            res.add(cur.val);
            cur = cur.right;
        }
    }
}
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postOrderStack(root, res);
        return res; 
    }
    private void postOrderRecursive(TreeNode root, List res) {
        if (root == null) return;

        postOrderRecursive(root.left, res);
        postOrderRecursive(root.right, res);
        res.add(root.val);
    }

    private void postOrderStack(TreeNode root, List res) {
        if (root == null) return;

        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            res.add(cur.val);
            if (cur.left != null) {
                stack.push(cur.left);
            }

            if (cur.right != null) {
                stack.push(cur.right);
            }
        }

        Collections.reverse(res);
    }
}
```
