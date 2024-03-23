# Day 16: 代码随想录算法训练营

## Topic:
- Binary Tree
- DFS
- BFS

## Summary:
- 用不同的遍历顺序 解决不同的问题
- 今天的题有难度， 主要还是考察自己的逻辑和细节的把控
- 递归三要素
  - 返回值和参数
  - 终止条件
  - 单层递归逻辑（有时候脑子没有必要一定要全部过一遍， 单层逻辑能过就可以了。不然脑子cpu不够用的）

[Recourse](https://programmercarl.com/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.html)

## Leetcode Problem

Leetcode 112. 路径总和
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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return helper(root, 0, targetSum);
    }

    private boolean helper(TreeNode root, int curSum, int target) {
        if (root == null) {
            return false;
        }
        
        curSum += root.val;
        
        // Check if the current node is a leaf and if the path sum equals the target sum
        if (root.left == null && root.right == null) {
            return curSum == target;
        }
        boolean left = helper(root.left,curSum, target);
        boolean right = helper(root.right, curSum, target);


        return left || right;

    }
}
```

Leetcode 113 路径总和 II
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
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<>();
        helper(root, res, path, targetSum);
        return res;
    }

    private void helper(TreeNode root, List<List<Integer>> res, List<Integer> path, int target) {
        if (root == null) return ;

        path.add(root.val);

        if (root.left == null && root.right == null) {
            int sum = path.stream().reduce(0, Integer::sum);
            if (sum == target) {
                res.add(new ArrayList<>(path));
            }
            return;
        }

        if (root.left != null) {
            helper(root.left, res, path, target);
            path.remove(path.size() - 1);
        }
        if (root.right != null) {
            helper(root.right, res, path, target);
            path.remove(path.size() - 1);
        }
    }
}
```

Leetcode 513 找树左下角的值
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
    public int findBottomLeftValue(TreeNode root) {
        int res = 0;
        Deque<TreeNode> que = new LinkedList<>();
        que.offer(root);
        while (!que.isEmpty()) {
            int size = que.size();

            for (int i = 0; i < size; i++) {
                TreeNode cur = que.poll();
                if (i == 0) res = cur.val;
                if (cur.left != null) que.offer(cur.left);
                if (cur.right !=null) que.offer(cur.right);
            }
        }

        return res;
    }
}
```

Leetcode 106 从中序与后序遍历序列构造二叉树
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
    int postIndex;
    HashMap<Integer, Integer> inorderIndexMap = new HashMap<>();
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        postIndex = postorder.length - 1;

        // val -> index   inorder 
        for (int i = 0; i < inorder.length; i++) {
            inorderIndexMap.put(inorder[i], i);
        }

        return buildTree(inorder, postorder, 0, postIndex);
    }
    /**
    用后序找根节点
    然后用根节点在中序里面找左右子树
    小问题解决大问题
     */
    private TreeNode buildTree(int[] inorder, int[] postorder, int start, int end) {
        if (start > end) return null;

        TreeNode root = new TreeNode(postorder[postIndex--]);
        int index = inorderIndexMap.get(root.val);
        
        root.right = buildTree(inorder, postorder, index + 1, end);
        root.left = buildTree(inorder, postorder, start, index - 1);

        return root;
    }
}
```
