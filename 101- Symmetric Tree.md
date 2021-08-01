# 101. Symmetric Tree

**# 101. Symmetric Tree**

**_## Iteration_**

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root.left);
        queue.offer(root.right);
        
        while (!queue.isEmpty()) {
            TreeNode currL = queue.poll();
            TreeNode currR = queue.poll();
            
            if (currL == null && currR == null) continue;
            if (currL == null || currR == null || currL.val != currR.val) return false;
            
            queue.offer(currL.left);
            queue.offer(currR.right);
            queue.offer(currL.right);
            queue.offer(currR.left);
        }
        
        return true;
    }
}

**_Recursive_**

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null)   return true;
        
        return helper(root.left, root.right);
    }
    
    private boolean helper(TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;       
        if (left == null || right == null || left.val != right.val) return false;
        
        return helper(left.left, right.right) && helper(left.right, right.left);
    }
}
