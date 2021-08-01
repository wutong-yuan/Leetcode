# Approach 1: order level traversal — use queue

# 

**Approach 1: order level traversal — use queue**
**
**
**I used the Pair class, below there is code for not using Pair class**

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
class Pair {
    TreeNode node;
    int depth;

    public Pair(TreeNode node, int depth) {
        this.depth = depth;
        this.node = node;
    }
}

class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        int depth = 0;
        Queue<Pair> queue = new LinkedList<>();
        
        queue.offer(new Pair (root, 1));
        
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            TreeNode node = pair.node;
            depth = pair.depth;
            if (node.left == null && node.right == null) {
                return depth;
            }
            if (node.left != null) {
                queue.offer(new Pair(node.left, depth + 1));                
            } 
            if (node.right != null) {
                queue.offer(new Pair(node.right, depth + 1));
            }
        }
        
        return 0;
    }
}

**_Not use pair class:_**
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int depth = 1;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left == null && node.right == null) {
                    return depth;
                }
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            depth++;
        }
        
        return depth;
    }
}

**_Recursive — DFS_**
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        if (root.left == null) return minDepth(root.right) + 1;
        if (root.right == null) return minDepth(root.left) + 1;
        
        return Math.min(minDepth(root.left) + 1,
                       minDepth(root.right) + 1);
    }
}

![Approach 1- order level traversal — use queue](images/Approach%201-%20order%20level%20traversal%20—%20use%20queue.png)

