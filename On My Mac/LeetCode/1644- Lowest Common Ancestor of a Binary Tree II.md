# 1644. Lowest Common Ancestor of a Binary Tree II

**1644. Lowest Common Ancestor of a Binary Tree II**

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
    boolean pFound = false;
    boolean qFound = false;
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {        
        TreeNode LCA = LCA(root, p, q);
        if (pFound && qFound) {
            return LCA;
        }
        return null;       
    }
    
    public TreeNode LCA (TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return root;
        
        TreeNode left = LCA(root.left, p, q);
        TreeNode right = LCA(root.right, p, q);
        
        if (root == p) {
            pFound = true;
            return root;
        }
        
        if (root == q) {
            qFound = true;
            return root;
        }
        if (left == null && right == null) return null;
        if (left != null && right != null) return root;
        if(left!= null) return left;
        if(right != null) return right;
        return null;
    }   
} 

![1644- Lowest Common Ancestor of a Binary Tree II](images/1644- Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree%20II.png)

![1644- Lowest Common Ancestor of a Binary Tree II-1](images/1644- Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree%20II-1.png)

