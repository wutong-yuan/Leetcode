# 222. Count Complete Tree Nodes

**222. Count Complete Tree Nodes**

![222- Count Complete Tree Nodes](images/222- Count%20Complete%20Tree%20Nodes.png)

https://www.youtube.com/watch?v=CvrPf1-flAA 

https://leetcode.com/problems/count-complete-tree-nodes/discuss/61958/Concise-Java-solutions-O(log(n)2)

## A very legible Solution for beginers
## 

class Solution {
    public int countNodes(TreeNode root) {
        if(root == null) return 0;
        
        int left = getHeightLeft(root);
        int right = getHeightRight(root);
        
        //If left and right are equal it means that the tree is complete and hence go for 2^h -1.
        if(left == right) return ((2<<(left)) -1);
            
        //else recursively calculate the number of nodes in left and right and add 1 for root.
        else return countNodes(root.left)+ countNodes(root.right)+1;
    }
    
    
    public int getHeightLeft(TreeNode root){
        int count=0;
        while(root.left!=null){
            count++;
            root = root.left;
        }
        return count;
    }
    
    
    public int getHeightRight(TreeNode root){
        int count=0;
        while(root.right!=null){
            count++;
            root = root.right;
        }
        return count;
    }
}

