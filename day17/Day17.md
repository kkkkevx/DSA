# Day 17: 代码随想录算法训练营

## Topic:
- Binary Tree
- BST
- DFS
- BFS

## Summary:
- 今天的题都还算简单， 二叉树有一点点小小心得 能很快找到思路。
- 还是一样继续熟悉 递归三部曲 好用
- java中一点之前不理解的语法点 ：     if else条件 else里面有return 外面就不用需要返回值 只用了if 外面需要有返回值
- BST 没有重复数

## Leetcode Problem
[Recourse](https://leetcode.cn/problems/maximum-binary-tree/)

Leetcode 654 最大二叉树
``` java
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
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return buildTree(nums, 0, nums.length - 1);
    }

    private TreeNode buildTree(int[] nums, int left, int right) {
        if (left > right) return null;

        int maxValueIndex = left;
        for (int i = left + 1; i <= right; i++) {
            if (nums[i] > nums[maxValueIndex]) maxValueIndex = i;
        }

        TreeNode root = new TreeNode(nums[maxValueIndex]);

        root.left = buildTree(nums, left, maxValueIndex - 1);
        root.right = buildTree(nums, maxValueIndex + 1, right);

        return root;
    }
}
```

Leetcode 617 合并二叉树
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
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        return buildTree(root1, root2);
    }
    /**
    递归终止条件要多想一下
    
     */
    private TreeNode buildTree(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;

        root1.val += root2.val;

        root1.left = buildTree(root1.left, root2.left);
        root1.right = buildTree(root1.right, root2.right);

        return root1;
    }
}
```

Leetcode 700 二叉搜索树中的搜索
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
    // 递归，利用二叉搜索树特点，优化
    /**
    if else条件 else里面有return 外面就不用需要返回值 只用了if 外面需要有返回值
     */
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null || root.val == val) {
            return root;
        }
        if (val < root.val) {
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
    }
}
```

Leetcode 98 验证二叉搜索树
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
    // public boolean isValidBST(TreeNode root) {
    //     List<Integer> list = new ArrayList<>();
    //     traversal(list, root);

    //     for (int i = 1; i < list.size(); i++) {
    //         if (list.get(i) <= list.get(i - 1)) return false;
    //     }
    //     return true;
    // }

    // private bo traversal(List<Integer> list, TreeNode root) {
    //     if (root == null) return;

    //     traversal(list, root.left);
    //     list.add(root.val);
    //     traversal(list, root.right);
    // }

    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean isValidBST(TreeNode root, long min, long max) {
        if (root == null) return true;
        if (root.val <= min || root.val >= max) return false;
        return isValidBST(root.left, min, root.val) && isValidBST(root.right, root.val, max);

    }
}
```

