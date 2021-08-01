# 145 Binary Tree Postorder Traversal

# 145 **# Binary Tree Postorder Traversal**# 

**_Iterative approach - see paper notes for details_**

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
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> postorderList = new ArrayList<>();
        
        if(root == null) return postorderList;
        
        stack.push(root);
        while(!stack.isEmpty()) {
            TreeNode current = stack.pop();
            postorderList.add(0, current.val);
            if(current.left != null) {
                stack.push(current.left);
            }
            if(current.right != null) {
                stack.push(current.right);
            }
        }
        return postorderList;
    }
}

**_Recursive DC_**

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> postorderList = new ArrayList<>();
        Stack<Integer> stack = new Stack<>();
        
        if(root == null) return postorderList;
        
        List<Integer> left = postorderTraversal(root.left);
        List<Integer> right = postorderTraversal(root.right);
        
        postorderList.addAll(left);
        postorderList.addAll(right);
        postorderList.add(root.val);
        
        return postorderList;
    }
}

**_Recursive - traversal_**

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> postorderList = new ArrayList<>();
        Stack<Integer> stack = new Stack<>();
        if(root == null) return postorderList;
        
        traversal(root, postorderList);
        return postorderList;
    }
    public void traversal(TreeNode root, List<Integer> postorderList) {
        if(root == null) return;
        
        traversal(root.left, postorderList);
        traversal(root.right, postorderList);
        postorderList.add(root.val);
        
        }
}

