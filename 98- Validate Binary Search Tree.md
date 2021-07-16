# 98. Validate Binary Search Tree

**98. Validate Binary Search Tree **

https://www.youtube.com/watch?v=s6ATEkipzow 

![98- Validate Binary Search Tree](images/98- Validate%20Binary%20Search%20Tree.png)

 

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
    public boolean isValidBST(TreeNode root) {
        return validBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    public boolean validBST(TreeNode node, long leftBound, long rightBound) {
        if(node == null) return true;
        
        if(!(node.val < rightBound && node.val > leftBound)) {
            return false;
        }
        
        boolean isLeftBST = validBST(node.left, leftBound, node.val);
        boolean isRightBST = validBST(node.right, node.val, rightBound);
        
        if(isLeftBST && isRightBST) return true;
        return false;
    }
}

Another approach is to use inroder traversal. See 230 notes 
https://leetcode.com/problems/validate-binary-search-tree/discuss/32112/Learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-(Java-Solution) 

![98- Validate Binary Search Tree-1](images/98- Validate%20Binary%20Search%20Tree-1.png)

