# 437. Path Sum III

**# 437. Path Sum III**
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
    public int pathSum(TreeNode root, int targetSum) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);        
        return dfs(root, map, targetSum, 0);
    }
    
    private int dfs(TreeNode root, Map<Integer, Integer> map, int targetSum, int currentSum) {
        if (root == null) return 0;
        
        currentSum += root.val;
        
        int count = map.getOrDefault(currentSum - targetSum, 0);
        map.put(currentSum, map.getOrDefault(currentSum, 0) + 1);
        
        
        count += dfs(root.left, map, targetSum, currentSum) + 
                dfs(root.right, map, targetSum, currentSum);
        
        map.put(currentSum, map.get(currentSum) - 1);  
        return count;
    }
}
