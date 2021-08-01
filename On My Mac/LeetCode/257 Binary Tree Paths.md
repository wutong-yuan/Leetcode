# 257 Binary Tree Paths

**_Recursion DC_**

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> paths = new ArrayList<>();
        if(root == null) return paths;
        if(root.left == null && root.right == null) {
            paths.add("" + root.val);
        }
        
        
        List<String> left = binaryTreePaths(root.left);
        List<String> right = binaryTreePaths(root.right);
        
        for(String path : left) {
            paths.add(root.val + "->" + path );
        }
        
        for(String path : right) {
            paths.add(root.val + "->" + path );
        }
        
        return paths;
    }
}

**_Another style:_**
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> answer = new ArrayList<>();
        if(root == null) return answer;
        searchBT(root, "", answer);
        return answer;
    }
    
    public void searchBT(TreeNode root, String path, List<String> answer) {
        if(root == null) return;
        if(root.left == null && root.right == null) {
            answer.add(path + root.val);
        }
        searchBT(root.left, path + root.val + "->" , answer);
        searchBT(root.right, path + root.val + "->", answer);
    }
}

![257 Binary Tree Paths](images/257%20Binary%20Tree%20Paths.png)

