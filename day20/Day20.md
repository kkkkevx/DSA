# Day 20: 代码随想录算法训练营

## Topic:
- Binary Search Tree
- BST
- DFS

## Summary;
- 有时候做题缺少一个耐心 无法沉下心去思考。急于找到正解。然而当基本知识都掌握了，思考的过程才是最宝贵。
- 就像538题不难，理解累加树的概念， 找到图中的便利顺序便能一次AC


## Leetcode:
[Recourse](https://programmercarl.com/0669.%E4%BF%AE%E5%89%AA%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.html)

Leetcode 669
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
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) return root;
        // 找到【low, high】范围内的值
        if (root.val < low) {
            TreeNode left = trimBST(root.right, low, high);
            return left;
        }
        if (root.val > high) {
            TreeNode right = trimBST(root.left, low, high);
            return right;
        }

        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

Leetcode 108
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
    public TreeNode sortedArrayToBST(int[] nums) {
        TreeNode root = buildTree(nums, 0, nums.length - 1);
        return root;
    }
    private TreeNode buildTree(int[] nums, int left, int right) {
        if (left > right) return null;
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = buildTree(nums, left, mid - 1);
        root.right = buildTree(nums, mid + 1, right);
        return root;
    }
}
```

Leetcode 538
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
    int pre = 0;
    public TreeNode convertBST(TreeNode root) {
        buildGST(root);
        return root;
    }

    private void buildGST(TreeNode root) {
        if (root == null) return;
        buildGST(root.right);
        pre += root.val;
        root.val = pre;
        buildGST(root.left);
    }
}
```
