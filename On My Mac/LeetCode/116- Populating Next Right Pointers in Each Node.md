# 116. Populating Next Right Pointers in Each Node

**# 116. Populating Next Right Pointers in Each Node**

# 

See leetcode article for details 
**_Approach 1 use queue to do BFS_**
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()) {
            int size = queue.size();
            
            // we need to keep i < size here instead of i < size -1 because we need to 
            // poll all the nodes in the current level and add all their children
            for (int i = 0; i < size; i++) {
                Node current = queue.poll(); 
               // here for the last node in the current level, it should point to null
                // if we don't do i < size -1, the last node will point to to the first node 
                // on the next level
                if(i < size - 1) {
                    current.next = queue.peek();
                }
                // we can only check if left is null because this is a pefect binary 
                // search tree
                if(current.left != null) {
                    queue.offer(current.left);
                    queue.offer(current.right);
                }                
            }            
        }
        return root;
    }
        
}

**_Iteration without using extra space_**

class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        Node leftmost = root;

        while (leftmost.left != null) {
            Node current = leftmost;
            while (current != null) {
                current.left.next = current.right;
                if(current.next != null) {
                    current.right.next = current.next.left;
                }
                current = current.next;
            }
        leftmost = leftmost.left;
        }

        return root;
    }
}

![116- Populating Next Right Pointers in Each Node](images/116- Populating%20Next%20Right%20Pointers%20in%20Each%20Node.png)

