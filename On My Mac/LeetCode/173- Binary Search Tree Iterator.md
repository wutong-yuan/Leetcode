# 173. Binary Search Tree Iterator

**# 173. Binary Search Tree Iterator **
**
**
**_First approach -_** use an array to store the inorder traversal results, which would be a sorted order.  Then we can implement the next ant hasNext very easy.
class BSTIterator {
    ArrayList<TreeNode> inorderList;
    int index;

    public BSTIterator(TreeNode root) {
        this.inorderList = new ArrayList<>();
        index = -1;
        inorderTraversal(root);      
    }
    
    private void inorderTraversal(TreeNode root) {
        if (root == null) return;
        
        inorderTraversal(root.left);
        this.inorderList.add(root);
        inorderTraversal(root.right);
    }
    
    public int next() {
        this.index++;
        return this.inorderList.get(this.index).val;
    }
    
    public boolean hasNext() {
        if (this.index + 1 < this.inorderList.size()) {
            return true;
        }
        return false;
    }
}

**_Second approach _**- use the stack for the next. We store the very left elements first. If the next() call an element which has a right child, we recursively call the right tree. 

	
