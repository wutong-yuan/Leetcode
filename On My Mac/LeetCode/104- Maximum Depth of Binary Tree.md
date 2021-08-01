# 104. Maximum Depth of Binary Tree

**104. Maximum Depth of Binary Tree**

**Recursive - DC**
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
    public int maxDepth(TreeNode root) {
        int maxDepth = 0;
        if (root == null) return 0;
        
        maxDepth = 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
        
        return maxDepth;
     
    }
}

Or:
 public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }

**_Recursive - traversal_**
class Solution {
    
   ** private int depth; // put a global variabe**

    
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        depth = 0;       
        traversal(root, 1);
        return depth;      
    }
    
    public void traversal(TreeNode root, int currentDepth) {
        if(root == null) return;
        
        if(currentDepth > depth) {
            depth = currentDepth;
        }
        
        traversal(root.left, currentDepth + 1);
        traversal(root.right, currentDepth + 1);
    }
}

**_Iterative _**

class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        Stack<TreeNode> stack = new Stack<>();
        Stack<Integer> depth = new Stack<>(); 
        int maxDepth = 0;
        int currentDepth = 1;
        
        stack.push(root);
        depth.push(currentDepth);
        
        while(!stack.isEmpty()) {
            TreeNode currentNode = stack.pop();
            currentDepth = depth.pop();
            maxDepth = Math.max(currentDepth, maxDepth);
            
            if(currentNode.right != null) {
                stack.push(currentNode.right);
                depth.push(currentDepth + 1);
            } 
            
            if(currentNode.left != null) {
                stack.push(currentNode.left);
                depth.push(currentDepth + 1);
            }
        }
        return maxDepth;
    }
}
