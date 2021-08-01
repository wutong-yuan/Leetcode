# My solution - would use extra space for the arraylist

# 

**_My solution - would use extra space for the arraylist_**
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        
        ArrayList<TreeNode> inorderList = new ArrayList<>();
        inorderTraversal(root, inorderList);
        
        int index = inorderList.indexOf(p);
        if (index + 1 >= inorderList.size()) return null;
        return inorderList.get(index + 1);     
    }
    
    public void inorderTraversal(TreeNode root, ArrayList<TreeNode> list ) {
        if (root == null) return;
        
        inorderTraversal(root.left, list);
        list.add(root);
        inorderTraversal(root.right, list);
    }
}

https://www.youtube.com/watch?v=5cPbNCrdotA&t=776s 
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(!findNode(root, p)) return null;
        
        if(p.right != null) {
            return findMin(p.right);
        } else {
            TreeNode successor = null;
           
            while (p != root) {
                if(p.val < root.val) {
                    successor = root;
                    root = root.left;
                } else {
                    root = root.right;
                }   
            }
            return successor;
        }

    }
    
    private TreeNode findMin(TreeNode root) {
        if (root == null) return null;
        
        while (root.left != null) {
            root = root.left;
        }
        return root;
    }
    
    private boolean findNode(TreeNode root, TreeNode node) {
        if (node == null) return false;
        
        while (root != null ){
            if (node.val > root.val) {
                root = root.right;
            } else if (node.val < root.val){
                root = root.left;
            } else {
                return true;
            }
        }
        return false;        
    }

**_Recursion_** 

https://leetcode.com/problems/inorder-successor-in-bst/discuss/72653/Share-my-Java-recursive-solution 

Both predecessor and successor
**## Successor**## 

## 

public TreeNode successor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val <= p.val) {
    return successor(root.right, p);
  } else {
    TreeNode left = successor(root.left, p);
    return (left != null) ? left : root;
  }
}
## 

**## Predecessor**## 

## 

public TreeNode predecessor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val >= p.val) {
    return predecessor(root.left, p);
  } else {
    TreeNode right = predecessor(root.right, p);
    return (right != null) ? right : root;
  }
}
 

}
