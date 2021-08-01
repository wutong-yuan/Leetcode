# 95. Unique Binary Search Trees II

**# 95. Unique Binary Search Trees II**

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
    public List<TreeNode> generateTrees(int n) {
        return helper(1, n);        
    }
    
    private List<TreeNode> helper(int start, int end) {
        List<TreeNode> result = new ArrayList<>();
        if (start > end) {
            result.add(null);
        }
        
        for (int i = start; i <= end; i++) {
            List<TreeNode> leftList = helper(start, i - 1);
            List<TreeNode> rightList = helper(i + 1, end);
            // for each node in the left or right list, it is a treeNode list
            // when we do root.right = right (the right is a list of nodes, if you 
            // click it int he treeNode you would see its left or right node)
            for (TreeNode left : leftList) {
                for (TreeNode right : rightList) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    result.add(root);
                }
            }
        }
        
        return result;
    }
}

![95- Unique Binary Search Trees II](images/95- Unique%20Binary%20Search%20Trees%20II.png)

![95- Unique Binary Search Trees II-1](images/95- Unique%20Binary%20Search%20Trees%20II-1.png)

