# 146. LRU Cache

**# 146. LRU Cache**

https://www.youtube.com/watch?v=xDEuM5qa0zg 
https://www.youtube.com/watch?v=akFRa58Svug 

class LRUCache {
    // implementation with doubly linked list 
    //put most recently used element right after the head 
    
    class Node {
        int val;
        int key;
        Node prev;
        Node next;
        
        public Node(int key, int val) {
            this.val = val;
            this.key = key;
        }
    }
    
    Map<Integer, Node> map = new HashMap<>();
    int capacity;
    Node head = new Node(0, 0);
    Node tail = new Node(0, 0);

    public LRUCache(int capacity) {
        this.capacity = capacity;
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if(map.containsKey(key)) {
            Node node = map.get(key);
            // remove node from the doubly linked list
            remove(node);
            // insert it right after the head because this is the most recently touched node
            insert(node);
            return node.val;
        } else {
            return -1;
        }
    }
    
    public void put(int key, int value) {
        // if the map contains this key, meaning this node already exists in 
        // the double linked list, we need to remove it
        // if the map does not contain this key, we don't need to remove it.
        if(map.containsKey(key)) {
            Node node = map.get(key);
            remove(node);
        }
        //before we put the new node into the list we need to check if the list is full
        // if it is full, we need to remove the one before the tail because 
        // that is the least recently used node
        if(map.size() == capacity) {
            remove(tail.prev);
        }
        Node newNode = new Node(key, value);
        insert(newNode);
    }
    
    private void remove(Node node) {
        map.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void insert(Node node) {
        map.put(node.key, node);
        node.next = head.next;
        node.next.prev = node;
        head.next = node;
        node.prev = head; 
    }
    
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
