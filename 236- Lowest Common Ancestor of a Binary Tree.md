# 236. Lowest Common Ancestor of a Binary Tree

**236. Lowest Common Ancestor of a Binary Tree**

https://www.youtube.com/watch?v=13m9ZCB8gjw 

![236- Lowest Common Ancestor of a Binary Tree](images/236- Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree.png)

![236- Lowest Common Ancestor of a Binary Tree-1](images/236- Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree-1.png)

![236- Lowest Common Ancestor of a Binary Tree-2](images/236- Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree-2.png)

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
        if(root == null) return null;
        
        if(root == p || root == q) return root;
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left == null && right == null) return null;
        if (left != null && right != null) return root;
        if(left!= null) return left;
        if(right != null) return right;
        
        return null;
    }
}

