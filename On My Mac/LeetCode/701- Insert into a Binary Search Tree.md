# 701. Insert into a Binary Search Tree

**# 701. Insert into a Binary Search Tree **

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode newNode = new TreeNode(val);
        if (root == null) {
            return newNode;
        }
        
        TreeNode temp = root;
        while (true) {
            if(val < temp.val) {
                if(temp.left == null) {
                    temp.left = newNode;
                    break;
                }else {
                    temp = temp.left;
                }
            } else {
                if (temp.right == null) {
                    temp.right = newNode;
                    break;
                } else {
                    temp = temp.right;
                }
            }       
        }        
        return root;
    }
}

**_Recursive_**

class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        if(val < root.val) {
            root.left = insertIntoBST(root.left, val);
        } else if (val > root.val) {
            root.right = insertIntoBST(root.right, val);
        }  
        
        return root;
    }
}

