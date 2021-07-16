# 99. Recover Binary Search Tree

**# 99. Recover Binary Search Tree**
**
**
**https://www.youtube.com/watch?v=LR3K5XAWV5k&t=513s**** **
**
**
If we do inorder traversal, the following element should be bigger than the previous one. Otherwise, it is the one we are looking for. Usually we would have two pairs, like the example below. 15, 7 and 14, 5. But if the two swapped elements are next to each other, we would have only one pair, like the second example. **
**
**
**
**
**
![99- Recover Binary Search Tree](images/99- Recover%20Binary%20Search%20Tree.png)

![99- Recover Binary Search Tree-1](images/99- Recover%20Binary%20Search%20Tree-1.png)**
**
**
**
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
    TreeNode firstElement;
    TreeNode secondElement;
    TreeNode previousElement;   
    
    public void recoverTree(TreeNode root) {
        if (root == null) return;
        
        inorderTraversal(root);
        
        int temp = firstElement.val;
        firstElement.val = secondElement.val;
        secondElement.val = temp;
    }
    
    public void inorderTraversal(TreeNode root) {
        if (root == null) return;
        
        inorderTraversal(root.left);
        
        if(previousElement != null) {
            if(previousElement.val > root.val) {
            if(firstElement == null) {
                firstElement = previousElement;
            }
            secondElement = root;
            }       
        }     
        previousElement = root;
        inorderTraversal(root.right);
    }
}
