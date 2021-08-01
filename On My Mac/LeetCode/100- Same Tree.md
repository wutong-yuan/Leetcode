# 100. Same Tree

**# 100. Same Tree**

Approach 1: Recursive 

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        
        if (p.val == q.val) {
            return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
        }
        return false;
    }
}

**_Approach 2: Iteration using queue_**
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> queue = new LinkedList<>();
        
        queue.offer(p);
        queue.offer(q);
        
        while (!queue.isEmpty()) {
            TreeNode currP = queue.poll();
            TreeNode currQ = queue.poll();
            
           ** if (currP == null && currQ == null) {**
**                continue; **

            } else if(currP == null || currQ == null || currP.val != currQ.val) {
                return false;
            }
            
            queue.offer(currP.left);
            queue.offer(currQ.left);
            queue.offer(currP.right);
            queue.offer(currQ.right);
        }
     return true;   
    }
}

![100- Same Tree](images/100- Same%20Tree.png)

