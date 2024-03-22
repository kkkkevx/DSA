# Day 15: 代码随想录算法训练营

## Topic:
- Binary Tree
- DFS
- BFS

## Summary:
- 前序算深度 top-down 后序算高度 bottom-up
- 左叶子，不是二叉树左侧节点。 节点A的左孩子不为空，且左孩子的左右孩子都为空（说明是叶子节点），那么A节点的左孩子为左叶子节点。
- 递归三部曲
  - 判断返回值和参数
  - 终止条件
  - 小问题的解决解决方案
- 回溯的核心思想： 试错，错了就回溯到上一次或者上上上次。
- 递归 解决树的问题 分而治之不用苦心于整体， 分解后能解决小问题就能解决大问题。A（n） = A(n-1) +1

## Leetcode Problem:

Leetcode 404. 左叶子之和

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
    public int sumOfLeftLeaves(TreeNode root) {
        return helper(root);
    }

    private int helper(TreeNode root) {
        if (root == null) return 0;
        int leftValue = helper(root.left);
        int rightValue = helper(root.right);

        int sum = 0;
        if (root.left != null && root.left.left == null && root.left.right == null) {
            sum += root.left.val;
        }
        return sum + leftValue + rightValue;
    }
}
```

Leetcode 257  二叉树的所有路径

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<Integer> path = new ArrayList<>();
        List<String> res = new ArrayList<>();
        helper(root, path, res);
        return res;
    }

    private void helper(TreeNode root, List<Integer> path, List<String> res) {
        path.add(root.val);
        if (root.left == null && root.right == null) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < path.size() - 1; i++) {
                sb.append(path.get(i)).append("->");
            }
            sb.append(path.get(path.size()-1));
            res.add(sb.toString());
        }

        if (root.left != null) {
            helper(root.left, path, res);
            path.remove(path.size()-1);
        }
        if (root.right != null) {
            helper(root.right, path, res);
            path.remove(path.size()-1);
        }
    }
}
```

Leetcode110. 平衡二叉树
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
    public boolean isBalanced(TreeNode root) {
         return postOrder(root) != -1;
    }

    private int postOrder(TreeNode root) {
        if (root == null) return 0;

        int left = postOrder(root.left);
        if (left == -1) return -1;
        int right = postOrder(root.right);
        if (right == -1) return -1;

        int result = Math.abs(left - right);
        if (result > 1) {
            result = -1;
        } else {
            result = Math.max(left, right) + 1;
        }
        return result;
    }
}
```
