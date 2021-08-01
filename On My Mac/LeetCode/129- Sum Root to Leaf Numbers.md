# 129. Sum Root to Leaf Numbers

**# 129. Sum Root to Leaf Numbers**

 
**_Recursive_**
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

    public int sumNumbers(TreeNode root) {
        if (root == null) return 0;
        return findSum(root, 0);        
    }
    
    private int findSum(TreeNode root, int sum) {
        if (root == null)  return 0;
        
        sum = sum * 10 + root.val;
        
        if (root.left == null && root.right == null) return sum;        
        sum = findSum(root.left, sum) + findSum(root.right, sum);
        
        return sum;
    }
}

**_Use pair and queue_**
class Pair {
    TreeNode node;
    int currentSum;
    
    public Pair(TreeNode node, int currentSum) {
        this.node = node;
        this.currentSum = currentSum;
    }
}

class Solution {
    public int sumNumbers(TreeNode root) {
        Queue<Pair> queue = new LinkedList<>();
        int sum = 0;
        
        queue.offer(new Pair(root, 0));
        while (!queue.isEmpty()) {
            Pair currPair = queue.poll();
            TreeNode currNode = currPair.node;
            int currSum = currPair.currentSum;
            
            currSum =  currSum * 10 + currPair.node.val;
            if (currNode.left == null && currNode.right == null) {
                sum += currSum;
            } else {
                if (currNode.left != null){
                    queue.offer(new Pair(currNode.left, currSum));
                }
                if (currNode.right != null) {
                    queue.offer(new Pair(currNode.right, currSum));
                }
            }
        }
        
        return sum;
    }
}

