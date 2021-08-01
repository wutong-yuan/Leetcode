# 113. Path Sum II

**# 113. Path Sum II**
# 

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
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        if (root == null) return result;
        helper(result, tempList, root, targetSum);
        return result;
    }
    
    private void helper(List<List<Integer>> result, List<Integer> tempList, TreeNode root, int targetSum) {
        if(root == null) return;
        
        tempList.add(root.val);
        if (root.left == null && root.right == null && targetSum == root.val) {
            result.add(new ArrayList<>(tempList));
        } else {
            if (root.left != null) helper(result, tempList, root.left, targetSum - root.val);
            if (root.right != null) helper(result, tempList, root.right, targetSum - root.val);
        }
        
        tempList.remove(tempList.size() - 1);
    }
}
