# 106. Construct Binary Tree from Inorder and Postorder Traversal

**# 106. Construct Binary Tree from Inorder and Postorder Traversal**

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
    int postorderIndex;
    
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        Map<Integer, Integer> inorderMap = new HashMap<>();
        postorderIndex = postorder.length - 1;
        
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        
        return helper(postorder, inorderMap, 0, inorder.length - 1);
    }
    
    private TreeNode helper(int[] postorder, Map<Integer, Integer> inorderMap, int start, int end) {
        if (start > end) return null;
        
        int rootVal = postorder[postorderIndex--];
        TreeNode root = new TreeNode(rootVal);
        int rootInorderIndex = inorderMap.get(rootVal);
        root.right = helper(postorder, inorderMap, rootInorderIndex + 1, end);
        root.left = helper(postorder, inorderMap, start, rootInorderIndex - 1);
        return root;
    }
}

