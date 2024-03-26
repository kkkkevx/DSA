# Day 18: 代码随想录算法训练营

## Topic:
- Binary Search Tree
- BST
- DFS

## Summary:
- 二叉树 前序自上而下遍历 后序 自下而上遍历
- 中序在二叉搜索树中， 是排序遍历
- 递归中如何记录前一个指针， 写一个全局变量在方法外。 Nice

## Leetcode Problem
[Recourse](https://programmercarl.com/0501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B0.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)

Leetcode 501
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
    private int Maxcount = 0;
    private int count = 0;
    private TreeNode pre = null;
    private List<Integer> list = new ArrayList<>();
    public int[] findMode(TreeNode root) {
        traversal(root);
        int[] res = list.stream().mapToInt(Integer::intValue).toArray();
        return res;
    }

    private void traversal(TreeNode root) {
        if (root == null) return;
        traversal(root.left);

        // 找众数
        if (pre == null || root.val != pre.val) {
            count = 1;
        } else {
            count++;
        }
        // 更新pre
        pre = root;

        // 有多个众数
        if (count == Maxcount) {
            list.add(root.val); 
        }
        // 找到更多的众数
        if (count > Maxcount) {
            Maxcount = count;
            list.clear();
            list.add(root.val);
        }
        traversal(root.right);
    }
}
```

Leetcode 530
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
    public int getMinimumDifference(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traversal(root, list);
        int min = Integer.MAX_VALUE;
        for (int i = 1; i< list.size(); i++) {
            int diff = list.get(i) - list.get(i-1);
            if (diff < min) min = diff;
        }

        return min;

    }

    private void traversal(TreeNode root, List list){
        if (root == null) return;

        traversal(root.left, list);
        list.add(root.val);
        traversal(root.right, list);
    }
}
```

Leetcode 236
用后序遍历 自下而上找公共祖先 找到后返回Node。 等都找到后返回root
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root == p || root == q) return root;

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) return root;

        if (left != null && right == null) {
            return left;
        } else if (left == null && right != null) {
            return right;
        } else {
            return null;
        }
    }
}
```
