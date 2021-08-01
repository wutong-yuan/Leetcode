# 124. Binary Tree Maximum Path Sum

**# 124. Binary Tree Maximum Path Sum**

# 

**_Not use global variable_**
https://www.youtube.com/watch?v=Hr5cWUld4vU 

class Solution {
    public int maxPathSum(TreeNode root) {
        if (root == null)   return 0;        
        int[] max = new int[1];
        max[0] = Integer.MIN_VALUE;
        findMax(root, max);     
        return max[0];
    }
    
    private int findMax(TreeNode root, int[] max) {
        if (root == null) return 0;        
        int leftMax = Math.max(findMax(root.left, max), 0);
        int rightMax = Math.max(findMax(root.right, max), 0);
        
        int rootMax = leftMax + rightMax + root.val;
        max[0] = Math.max(max[0], rootMax);
        
        return root.val + Math.max(leftMax, rightMax);        
    }
}

**_Approach 2 - use global variable_**
class Solution {
    int max = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        if (root == null)     return 0;
        findMax(root);
        return max;
    }
    
    private int findMax(TreeNode root) {
        if (root == null) return 0;
        int left = Math.max(findMax(root.left), 0);
        int right = Math.max(findMax(root.right), 0);
        
        int rootMax = left + right + root.val;
        max = Math.max(max, rootMax);
        return root.val + Math.max(left, right);
    }
}

![124- Binary Tree Maximum Path Sum](images/124- Binary%20Tree%20Maximum%20Path%20Sum.png)

![124- Binary Tree Maximum Path Sum-1](images/124- Binary%20Tree%20Maximum%20Path%20Sum-1.png)

