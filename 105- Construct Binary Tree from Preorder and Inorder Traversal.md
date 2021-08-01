# 105. Construct Binary Tree from Preorder and Inorder Traversal

**# 105. Construct Binary Tree from Preorder and Inorder Traversal**# 

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
    int index;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        
        return helper(preorder, 0, preorder.length - 1, map);
    }
    
    private TreeNode helper(int[] preorder, int leftStart, int rightEnd, Map<Integer, Integer> map) {
        if (leftStart > rightEnd) return null;
                
        
            int rootVal = preorder[index++];
            TreeNode root = new TreeNode(rootVal);
            int leftEnd = map.get(rootVal) - 1;
            int rightStart = map.get(rootVal) + 1;

            root.left = helper(preorder, leftStart, leftEnd, map);
            root.right = helper(preorder, rightStart, rightEnd,map);
        
        return root;                
    }
}

**_See paper notes for details of those two approaches_**
class Solution {
    
    int preorderIndex;
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inorderMap = new HashMap<>();
        
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        
        return helper(preorder, inorderMap, 0, inorder.length - 1);
    }
    
    private TreeNode helper(int[] preorder, Map<Integer, Integer> inorderMap, int inorderStart, int inorderEnd) {
        if (inorderStart > inorderEnd) {
            return null;
        }
        
        int currRootVal = preorder[preorderIndex];
        TreeNode currRoot = new TreeNode(currRootVal);
        preorderIndex++;
        int currRootInorderIndex = inorderMap.get(currRootVal);
        
        currRoot.left = helper(preorder, inorderMap, inorderStart, currRootInorderIndex - 1);
        currRoot.right = helper(preorder, inorderMap, currRootInorderIndex + 1, inorderEnd);
        
        return currRoot;
    }
}

https://www.youtube.com/watch?v=6Xcz08RkRHE 

![105- Construct Binary Tree from Preorder and Inorder Traversal](images/105- Construct%20Binary%20Tree%20from%20Preorder%20and%20Inorder%20Traversal.png)

