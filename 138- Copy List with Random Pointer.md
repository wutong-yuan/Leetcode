# 138. Copy List with Random Pointer

**138. Copy List with Random Pointer**
**
**
**_Use hashMap_**
**
**
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node, Node> map = new HashMap<>();
        
        Node current = head;
        while (current != null) {
            map.put(current, new Node(current.val));
            current = current.next;
        }
        
        // assgin next and random pointers
        Node oldNode = head;
        while (oldNode != null) {
            //next
            Node newNode = map.get(oldNode);
            Node oldNodeNext = oldNode.next;
            Node newNodeNext = map.get(oldNodeNext);
            newNode.next = newNodeNext;
            // random
            Node oldNodeRandom = oldNode.random;
            Node newNodeRandom = map.get(oldNodeRandom);
            newNode.random = newNodeRandom;
            
            // continue to the next
            oldNode = oldNode.next;
        }
        return map.get(head);
    }
}

/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

**_// use O(1) space_**
**_
_**
**_My code:_**
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        
        // create the next 1', 2' 3'
        // 1-1'-2-2'...
        Node oldNode = head;
        while (oldNode != null) {
            Node newNode = new Node(oldNode.val);
            Node oldNodeNext = oldNode.next;
            oldNode.next = newNode;
            newNode.next = oldNodeNext;
            
            oldNode = oldNodeNext;
        }        
        
        // create the random 
        oldNode = head;
        while (oldNode != null) {
            Node newNode = oldNode.next;
            if (oldNode.random != null) {
                Node oldRandom = oldNode.random;
                Node newRandom = oldRandom.next;
                newNode.random = newRandom;         
            } else {
                newNode.random = null;
            }  
            oldNode = oldNode.next.next;
        }
        
        // cut the new list out. restore the old list as well
        Node newHead = head.next;
        Node pointerNew = newHead;
        Node pointerOld = head;
        while (pointerOld != null) {
            pointerOld.next = pointerOld.next.next;
            if (pointerNew.next != null) {
                pointerNew.next = pointerNew.next.next;
            } else {
                pointerNew.next = null;
            }
            pointerOld = pointerOld.next;
            pointerNew = pointerNew.next;
        }
        
        return newHead;
    }
}**_
_**

**_Leetcode code_**
class Solution {
    
    public Node copyRandomList (Node head) {
        if (head == null) {
            return null;
        }
        Node ptr = head;
        while (ptr != null) {
            //create a new node A'
            Node newNode = new Node(ptr.val);
            //let the new node A' point to B
            newNode.next = ptr.next;
            // let the original head A point to A'
            // this will break the connection between A and B
            // this will generate A-->A'-->B-->
            ptr.next = newNode;
            // move to B and start the same process. Now B is the start
            ptr = newNode.next;
        }
        // After we finish the weave for the next pointers, we get 
        // A-->A'-->B-->B'-->C-->C'....
        // set the ptr to be the head because we will start the same 
        // process for the random pointers
        ptr = head;
        
        while (ptr != null) {
            // A-->A'-->B-->B'-->C-->C'....
            // Now ptr is A, ptr.next is A', ptr.next.random is A''s random pointer
            // let this pointer point to ptr.random.next, which is C'.
            // so A' random pointer points to C'
            ptr.next.random = (ptr.random != null) ? ptr.random.next : null;
            // then we move it to B, which is A's next next
            ptr = ptr.next.next;
        }
        //Unweave this linkedList to get back the original list and the cloned list
        // create a new node and assign head A to it
        Node ptr_old_list = head; 
        //create a new node and assign A' to it
        Node ptr_new_list = head.next;
        // create a new node and assign A' to it
        Node head_old = head.next;
        while (ptr_old_list != null) {
            // let A point to B
            ptr_old_list.next = ptr_old_list.next.next;
            // let A' point to B'
            ptr_new_list.next = (ptr_new_list.next !=nill) ? ptr_new_list.next.next : null;
            // move the start to B
            ptr_old_list = ptr_old_list.next;
            // move the start to B'
            ptr_new_list = ptr_new_list._next;
        }
        // head_old is A'
        return head_old;     
    }
    
}
