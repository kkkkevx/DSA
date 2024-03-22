# Day 14: 代码随想录算法训练营

## Topic:
- Binary Tree
- DFS
- BFS

## Summary:
- 前序求的就是深度，使用后序求的是高度。
  - 二叉树节点的深度：指从根节点到该节点的最长简单路径边的条数或者节点数（取决于深度从0开始还是从1开始）
  - 二叉树节点的高度：指从该节点到叶子节点的最长简单路径边的条数或者节点数（取决于高度从0开始还是从1开始）
- 一道题可能有多种解法 通过不同的遍历方法
- 之后二刷要掌握迭代法

## Leetcode Problem"
**[Recourse](https://programmercarl.com/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.html#%E6%80%9D%E8%B7%AF)**

Leetcode 104: 二叉树的最大深度
递归
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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

Leetcode 111： 二叉树的最小深度

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
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        int left = minDepth(root.left);
        int right = minDepth(root.right);

        if (root.left == null && root.right != null) return 1 + right;
        if (root.right == null && root.left != null) return 1 + left;
        return Math.min(left, right) + 1;
    }
}
```

Leetcode 222 完全二叉树的节点个数
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
    public int countNodes(TreeNode root) {
        //return bfsCount(root);
        return preOrderCount(root);
    }
    private int preOrderCount(TreeNode root) {
        if (root == null) return 0;
        return 1 + preOrderCount(root.left) + preOrderCount(root.right);
    }
    private int bfsCount(TreeNode root) {
        /**
        BFS
         */
        int res = 0;
        if (root == null) return res;

        Deque<TreeNode> que = new LinkedList<>();
        que.offer(root);

        while (!que.isEmpty()) {
            int size = que.size();
            while (size-- > 0) {
                TreeNode cur = que.poll();
                res++;
                if (cur.left != null) que.offer(cur.left);
                if (cur.right != null) que.offer(cur.right);
            }
        }
        return res;
    }
}
```
