# 94. Binary Tree Inorder Traversal

**94. Binary Tree Inorder Traversal**
**
**
**Binary tree traversal methods:**
**
**
**_Stack approach:_****
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
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> inorder = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        
        if(root == null) return inorder;
        TreeNode current = root;
        
        while(current != null || !stack.isEmpty()) {
            while(current != null) {
                //always push the root first. 1 is 2's root, 2 is 4's root
                stack.push(current);
                // then we set the current to left and keep pushing the left child
                current = current.left;
            }
            // we pop the top ones from the very left node 4 and add it to result
            current = stack.pop();
            inorder.add(current.val);
            // we move to the right cause if the right child has a subtree as well, 
            // we need to do the same thing like add all the left children first.
            // see paper notes example 2
            current = current.right;
        }
        return inorder;
    }
}

**_Recursion approach - DC:_**

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inorder = new ArrayList<>();
        if(root == null) return inorder;
        
        //divide
        List<Integer> left = inorderTraversal(root.left);
        List<Integer> right = inorderTraversal(root.right);
        
        inorder.addAll(left); // becareful about here. addAll
        inorder.add(root.val); // root is a node, we can add value only
        inorder.addAll(right);
        return inorder;
    }
}

**_Recursion approach - Traversal:_**

class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inorderList = new ArrayList<>();
        if(root == null) return inorderList;
        traversal(root, inorderList);
        return inorderList;
    }
    
    public void traversal(TreeNode root, List<Integer> inorderList) {
        if(root == null) return;	
        
        traversal(root.left, inorderList);
        inorderList.add(root.val);
        traversal(root.right, inorderList);       
    }
}**
**
**
**
**https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/**** **
**
**
![94- Binary Tree Inorder Traversal](images/94- Binary%20Tree%20Inorder%20Traversal.png)

Depth First Traversals: 
(a) Inorder (Left, Root, Right) : 4 2 5 1 3 
(b) Preorder (Root, Left, Right) : 1 2 4 5 3 
(c) Postorder (Left, Right, Root) : 4 5 2 3 1
Breadth First or Level Order Traversal : 1 2 3 4 5 

**_Iteration method_**
**_https://leetcode.com/problems/binary-tree-inorder-traversal/discuss/31213/Iterative-solution-in-Java-simple-and-readable_****_ _**
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();

    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode cur = root;

    while(cur!=null || !stack.empty()){
        while(cur!=null){
            stack.add(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        list.add(cur.val);
        cur = cur.right;
    }

    return list;
}

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode curr = root;
        TreeNode pre;
        while (curr != null) {
            // if current does not have left child
            if (curr.left == null) {
                // add current's value
                res.add(curr.val);
                // go to the right
                curr = curr.right;
            } else {
                // current has a left child, in the current's left subtree
                pre = curr.left;
                // find the right child of the rightmose node
                while (pre.right != null) {
                    pre = pre.right;
                }
                //make current the right child of the rightmost node
                pre.right = curr;
                //move to the current's left child
                TreeNode temp = curr;
                curr = curr.left;
                // original cur left be null, avoid infinite loops
                temp.left = null;
            }
        }
        return res;
    }
}

![94- Binary Tree Inorder Traversal-1](images/94- Binary%20Tree%20Inorder%20Traversal-1.png)

![94- Binary Tree Inorder Traversal-2](images/94- Binary%20Tree%20Inorder%20Traversal-2.png)

**
**

![94- Binary Tree Inorder Traversal-3](images/94- Binary%20Tree%20Inorder%20Traversal-3.png)

![94- Binary Tree Inorder Traversal-4](images/94- Binary%20Tree%20Inorder%20Traversal-4.png)

![94- Binary Tree Inorder Traversal-5](images/94- Binary%20Tree%20Inorder%20Traversal-5.png)

![94- Binary Tree Inorder Traversal-6](images/94- Binary%20Tree%20Inorder%20Traversal-6.png)

![94- Binary Tree Inorder Traversal-7](images/94- Binary%20Tree%20Inorder%20Traversal-7.png)

![94- Binary Tree Inorder Traversal-8](images/94- Binary%20Tree%20Inorder%20Traversal-8.png)

![94- Binary Tree Inorder Traversal-9](images/94- Binary%20Tree%20Inorder%20Traversal-9.png)

![94- Binary Tree Inorder Traversal-10](images/94- Binary%20Tree%20Inorder%20Traversal-10.png)

![94- Binary Tree Inorder Traversal-11](images/94- Binary%20Tree%20Inorder%20Traversal-11.png)

package com.yuanyuan;

import com.sun.source.tree.Tree;

public class TreeNode {

    int val;
    TreeNode left;
    TreeNode right;
    boolean rightThread;

    TreeNode() {
    }

    TreeNode(int val) {
        this.val = val;
    }

    TreeNode(int val, TreeNode left, TreeNode right, boolean rightThread) {
        this.val = val;
        this.left = left;
        this.right = right;
        this.rightThread = rightThread;
    }

    public static void main(String[] args) {
        TreeNode dummy = new TreeNode(-1);
        TreeNode ten = new TreeNode(10);
        TreeNode eight = new TreeNode(8);
        TreeNode twelve = new TreeNode(12);
        TreeNode fifteen = new TreeNode(15);
        TreeNode two = new TreeNode(2);
        TreeNode seven = new TreeNode(7);

        //Adding left and right child nodes
        ten.left = eight;
        ten.right = twelve;
        eight.left = fifteen;
        eight.right = two;
        two.left = seven;
        dummy.left = ten;
        dummy.right =dummy;
        dummy.rightThread = true;

        //Adding thread
        fifteen.right = eight;
        fifteen.rightThread = true;
        seven.right = two;
        seven.rightThread = true;
        two.right = ten;
        two.rightThread = true;
        twelve.right = dummy;
        twelve.rightThread = true;

        *inorder*(dummy);
    }

    //Returns inorder traversal
    public static void inorder(TreeNode node) {
        TreeNode curr = *leftmost*(node);
        //while node is not null and is not the dummy node
        while (curr != null && curr.val != -1) {
            //Process node
            System.*out*.println(curr.val + " ");
            //uPdate curr
            if (curr.rightThread) {
                curr = curr.right;
            } else {
                curr = *leftmost*(curr.right);
            }
        }
    }

    //Returns non-null leftmost child for the node
    private static TreeNode leftmost (TreeNode node) {
        if (node == null) {
            return null;
        }
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }
}

