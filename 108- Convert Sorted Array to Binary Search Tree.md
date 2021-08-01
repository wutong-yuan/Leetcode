# 108. Convert Sorted Array to Binary Search Tree

**# 108. Convert Sorted Array to Binary Search Tree**

Time complexity: O(N) since we visit each node exactly once.

Space complexity: O(N) to keep the output, and O(logN) for the recursion stack.

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
    public TreeNode sortedArrayToBST(int[] nums) {
        // in order traversal 
        
        return helper(nums, 0, nums.length - 1);       
    }
    
    private TreeNode helper(int[] nums, int start, int end) {
        if (start > end) return null;
        int mid = start + (end - start) / 2;
        
        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, start, mid - 1);
        root.right = helper(nums, mid + 1, end);
        
        return root;
    }
}
