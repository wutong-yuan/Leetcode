# 133. Clone Graph

**# 133. Clone Graph **

/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return node;
        //step1: get all the nodes in a list
        ArrayList<Node> nodes = getAllNodes(node);
        
        // step2: map the old nodes to new nodes
        // create a hashmap to store <oldNode, newNode>
        Map<Node, Node> mapping = new HashMap<>();
        for (Node oldNode : nodes) {
            // for each old node, we create its copy - new node
            // create a pair <oldNode, newNode>
            mapping.put(oldNode, new Node(oldNode.val));
        }
        
        //step3: copy the edges
        // add all neighbors for the new nodes
        // for each node in the old node list
        for (Node oldNode : nodes) {
            // find all its neighbors
            List<Node> oldNodeNeighbor = oldNode.neighbors;
            // for each neighbor of the old node, we need to create
            // the same neighbor for the new node
            // becareful, the new node needs to connect to the new 
            // neighbor. Not the old neighbors
            for (Node neighbor : oldNodeNeighbor) {
                // get the new node that corresponds to the old node
                Node newNode = mapping.get(oldNode);
                // get the new node that corresponds to the old neighbor
                Node newNodeNeighbor = mapping.get(neighbor);
                //connect the new neighbor to the new node
                newNode.neighbors.add(newNodeNeighbor);
            }    
        }
        // return the head of the new garph, which is the new node that 
        // corresponds to the old node
        return mapping.get(node);
    }
    
    private ArrayList<Node> getAllNodes(Node node) {
        Queue<Node> queue = new LinkedList<>();
        Set<Node> set = new HashSet<>();
        
        queue.offer(node);
        set.add(node);
        
        while(!queue.isEmpty()) {
            Node current = queue.poll();
            for (Node n : current.neighbors) {
                if (!set.contains(n)) {
                    set.add(n);
                    queue.offer(n);
                }
            }
        }
        
        return new ArrayList<>(set);
    }
    
}

