# 112. Path Sum

**# 112. Path Sum**
**
**
**
**
**_Recursive approach _**
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        if (root.left == null && root.right == null) return targetSum - root.val == 0;
        return hasPathSum(root.left, targetSum - root.val) || hasPathSum(root.right, targetSum - root.val);       
    }
    
    
}

**_Iteration using queue and pair_**

class Pair {
    
    TreeNode node;
    int target;
    
    public Pair(TreeNode node, int target) {
        this.node = node;
        this.target = target;
    }
}
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        Queue<Pair> queue = new LinkedList<>();
        queue.offer(new Pair(root, targetSum - root.val));
    
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            TreeNode node = pair.node;
            int reminder = pair.target;
            if (node.left == null && node.right == null && reminder == 0) return true;
            
            if (node.left != null) {                
                queue.offer(new Pair(node.left, reminder - node.left.val));
            }
            if (node.right != null) {
                queue.offer(new Pair(node.right, reminder - node.right.val));
            }
        }
      return false;              
    }
}
