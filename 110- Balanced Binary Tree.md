# 110. Balanced Binary Tree

**110. Balanced Binary Tree**

balanced binary tree: the difference between the heights of the two sub trees are not bigger than 1, and both the left sub tree and right sub tree are also balanced. 

**_With resultType_**

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
class ResultType {
    public boolean isBalanced;
    public int maxDepth;
    public ResultType(boolean isBalanced, int maxDepth) {
        this.isBalanced = isBalanced;
        this.maxDepth = maxDepth;
    }
}
class Solution {
    public boolean isBalanced(TreeNode root) {
        return helper(root).isBalanced;
    }
    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(true, 0);
        }
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        if(!left.isBalanced || !right.isBalanced) {
            return new ResultType(false, -1);
        }
        
        if(Math.abs(left.maxDepth - right.maxDepth) > 1) {
            return new ResultType(false, -1);
        }
        return new ResultType(true, Math.max(left.maxDepth, right.maxDepth) + 1);
    }
}

**_Without ResultType_**
**_
_**
**_https://leetcode.com/problems/balanced-binary-tree/discuss/35691/The-bottom-up-O(N)-solution-would-be-better_****_ 	_**

class Solution {
    
    public int depth (TreeNode root) {
        if (root == null) return 0;
        return Math.max(depth(root.left), depth(root.right)) + 1;
    }
    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        
        int left = depth(root.left);
        int right = depth(root.right);
        
        //Per balanced tree definition. two conditions
        return Math.abs(left - right) <= 1 &&
            isBalanced(root.left) && 
            isBalanced(root.right);
    }
}

Or:

class Solution {
    boolean isBalanced = true;
    public boolean isBalanced(TreeNode root) {
        if(root == null) return isBalanced;
        backtrack(root);
        return isBalanced;
    }
    private int backtrack(TreeNode root) {
        if(root == null) return 0;
        int left = backtrack(root.left);
        int right = backtrack(root.right);
        if(Math.abs(left - right) > 1) {
            isBalanced = false;
        }
        return Math.max(left, right) + 1;
    }
}

