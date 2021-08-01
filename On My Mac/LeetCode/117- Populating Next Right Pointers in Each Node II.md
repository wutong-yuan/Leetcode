# 117. Populating Next Right Pointers in Each Node II

**# 117. Populating Next Right Pointers in Each Node II**
# 

https://www.youtube.com/watch?v=W2xmj9ZYaHE

**_Approach 1 - not using extra space_**

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
        Node current = root;
        Node prev = null;
        Node headOfNextLevel = null;
        
        while (current != null) {
            while (current != null) {
                if (current.left != null) {
                    if (headOfNextLevel == null) {
                        headOfNextLevel = current.left;
                        prev = current.left;
                    } else {
                        prev.next = current.left;
                        prev = prev.next;
                    } 
                }
                if (current.right != null) {
                    if (headOfNextLevel == null) {
                        headOfNextLevel = current.right;
                        prev = current.right;
                    } else {
                        prev.next = current.right;
                        prev = prev.next;
                    }
                }
                current = current.next;
                }
            current = headOfNextLevel;
            prev = null;
            headOfNextLevel = null; 
            }            
            
        return root; 
    }
}

![117- Populating Next Right Pointers in Each Node II](images/117- Populating%20Next%20Right%20Pointers%20in%20Each%20Node%20II.png)

**_Use extra space : queue_**
class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
                Node current = queue.poll(); 
                if (i < size - 1) {
                    current.next = queue.peek();
                }
                if (current.left != null) {
                    queue.offer(current.left);
                }
                
                if(current.right != null) {
                    queue.offer(current.right);
                }
            }
        }
        
        return root;
    }
}
