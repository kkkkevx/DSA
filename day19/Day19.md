# Day 19: 代码随想录算法训练营

## Topic:
- Binary Search Tree
- BST
- DFS

## Summary:
- 在写递归的时候 对于返回值的处理还是不够熟练
- BST中找公共祖先第一个碰到的就是
- BST插入就是找空节点 插入
- BST删除 有五种可能
  - 没找到 直接返回
  - 左右节点都是空 就直接删除
  - 一个为空，另一个不为空 就返回不为空的节点 （左右各一种可能）
  - 左右节点都不为空，找中继节点做替换

## Leetcode Problem
[Recourse](https://programmercarl.com/0235.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88.html)

Leetcode 235
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
    /**
BST里面第一个在[p,q]范围里的就是 公共祖先
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
        if (root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);

        return root;
    }
}
```

Leetcode 701

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }

        if (val > root.val) {
            root.right = insertIntoBST(root.right, val);
        } else {
            root.left = insertIntoBST(root.left, val);
        }

        return root;
    }
}
```

Leetcode 450
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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return root;
        if (key > root.val) root.right = deleteNode(root.right, key);
        if (key < root.val) root.left = deleteNode(root.left, key);

        if (root.val == key) {
            if (root.left == null && root.right == null) {
                return null;
            } else if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            } else {

                TreeNode curParent = root;
                TreeNode cur = root.right;

                //找到中继节点
                while(cur.left != null) {
                    curParent = cur;
                    cur = cur.left;
                }

                // 找到中继节点并且中继节点的左节点为null 右节点不确定所有要把右节点给中继节点的父亲
                if (curParent != root) { //中继节点的父节点不是删除节点，把中继节点的右孩子给父节点的左节点
                    curParent.left = cur.right;
                } else { // 中继节点的父节点就是root， 把父节点的右节点变成中继节点的右节点
                    curParent.right = cur.right;
                }

                root.val = cur.val;
                return root;
            }
        }


        if (key > root.val) root.right = deleteNode(root.right, key);
        if (key < root.val) root.left = deleteNode(root.left, key);
        return root;
    }
}
```
