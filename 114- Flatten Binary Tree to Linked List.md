# 114. Flatten Binary Tree to Linked List

**# 114. Flatten Binary Tree to Linked List**# 

The leetnode notes is helpful too!

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
    public void flatten(TreeNode root) {
        if (root == null) return;
        helper(root);
    }
    
    public TreeNode helper(TreeNode root) {
        if(root == null) return null;
        if(root.left == null && root.right == null) return root;
        
        TreeNode leftTail = helper(root.left);
        TreeNode rightTail = helper(root.right);
        
        if(leftTail != null) {
            leftTail.right = root.right;
            root.right = root.left;
            root.left = null;   
        }
        
        return rightTail == null ? leftTail : rightTail;
    }
}

https://www.youtube.com/watch?v=pCtXQ9XI7As 

**_Approach 2 - use stack_**
class Solution {
    public void flatten(TreeNode root) {
        if (root == null) return;
        
        Stack<TreeNode> stack = new Stack<>();
        
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode curr = stack.pop();
            
            if(curr.right != null) {
                stack.push(curr.right);
            }
            if(curr.left != null) {
                stack.push(curr.left);
            }
            if(!stack.isEmpty()) {
                curr.right = stack.peek();
                curr.left = null;
            }
        }
    }
}

**_Approach 3 - Iterative _**
 public void flatten(TreeNode root) {
        
        // Handle the null scenario
        if (root == null) {
            return;
        }
        
        TreeNode node = root;
        
        while (node != null) {
            
            // If the node has a left child
            if (node.left != null) {
                
                // Find the rightmost node
                TreeNode rightmost = node.left;
                while (rightmost.right != null) {
                    rightmost = rightmost.right;
                }
                
                // rewire the connections
                rightmost.right = node.right;
                node.right = node.left;
                node.left = null;
            }
            
            // move on to the right side of the tree
            node = node.right;
        }
    }
}

