# 235. Lowest Common Ancestor of a Binary Search Tree

**# 235. Lowest Common Ancestor of a Binary Search Tree**
**
**
**_First approach - same as 236_**
**_
_**
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
        if (root == null) return null;
        if(root == p || root == q) {
            return root;
        }
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left == null && right == null) return null;
        if (left != null && right != null) return root;
        if (left != null) return left;
        if (right != null) return right;
        
        return null;
        
    }
}

**_Second approach: use binary search property_**
**_A non-recursive version._**

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // No edge check here because the constrains of this problem
        while (true) {
            // root.val is greater than both p.val and q.val. This means, p and q are 
            // both in the left tree. So we search the left.
            if (root.val > p.val && root.val > q.val) {
                root = root.left;
                // root.val is smaller than both p.val and q.val. This means, p and q
                // are both in the right tree. So we search the right.
            } else if (root.val < p.val && root.val < q.val) {
                root = root.right;
                // If one is smaller than root.val and one is bigger. 
                // Then root is their LCA
            } else {
                return root;
            }
        }
    }
}
**_Recursive version_**
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // No edge check here because the constrains of this problem
        while (true) {
            // root.val is greater than both p.val and q.val. This means, p and q are 
            // both in the left tree. So we search the left.
            if (root.val > p.val && root.val > q.val) {
                return lowestCommonAncestor(root.left, p, q);
                // root.val is smaller than both p.val and q.val. This means, p and q
                // are both in the right tree. So we search the right.
            } else if (root.val < p.val && root.val < q.val) {
                return lowestCommonAncestor(root.right, p, q);
                // If one is smaller than root.val and one is bigger. 
                // Then root is their LCA
            } else {
                return root;
            }
        }
    }
}
