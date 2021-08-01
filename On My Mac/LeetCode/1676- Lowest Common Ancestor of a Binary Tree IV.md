# 1676. Lowest Common Ancestor of a Binary Tree IV

**# 1676. Lowest Common Ancestor of a Binary Tree IV**
**
**
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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode[] nodes) {
        if(root == null) return null;
        for (int i = 0; i < nodes.length; i++) {
            if(root == nodes[i]) {
                return root;
            }
        }
        
        TreeNode left = lowestCommonAncestor(root.left, nodes);
        TreeNode right = lowestCommonAncestor(root.right, nodes);
        
        if(left != null && right != null) return root;
        if(left == null && right == null) return null;
        if(left != null) return left;
        if(right != null) return right;
        
        return null;
    }
}**
**
**
**
**
**
