# Lintcode 127  Topological Sorting

# Lintcode **# 127  **# Topological Sorting

**_From jiuzhang video4_**
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     List<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<DirectedGraphNode>();
 *     }
 * }
 */

public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // write your code here
        ArrayList<DirectedGraphNode> order = new ArrayList<>();

        if (graph == null) return order;

        // step 1: calculate the indegree: <node, indegree> 
        Map<DirectedGraphNode, Integer> indegreeMap = indegreeCal(graph);
        // step 2: get all the start node: indegree == 0. Could be mutilple nodes
        // so we need a list to store that 
        // since we will need the indegree == 0 info, we need two paramerters
        ArrayList<DirectedGraphNode> startNodeList = getStartNodes(graph, indegreeMap);

        // step 3: sort the graph starting from the indegree ==0 nodes 
        // each time, we cut those nodes out, add those nodes
        // to our result list, update its neigibor's degree
        // until all the nodes got cut
        order = sortBFS(startNodeList, indegreeMap);

        if (order.size() == graph.size()) {
            return order;
        }
        return null;
    }

    private Map<DirectedGraphNode, Integer> indegreeCal(ArrayList<DirectedGraphNode> graph) {
        Map<DirectedGraphNode, Integer> indegreeMap = new HashMap<>();
        // initialize this indegree map as <node, 0>. Indegree = 0 at the beginning
        for (DirectedGraphNode node : graph) {
            indegreeMap.put(node, 0);
        }
        // for each node in this graph, we check its neighbors. 
        // for its neighbors, since the current node is pointing to them, the 
        // neighbor's degree increment by 1
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                indegreeMap.put(neighbor, indegreeMap.get(neighbor) + 1);
            }
        }
        return indegreeMap;
    }

    private ArrayList<DirectedGraphNode> getStartNodes(ArrayList<DirectedGraphNode> graph,
                        Map<DirectedGraphNode, Integer> indegreeMap) {

        ArrayList<DirectedGraphNode> startNodeList = new ArrayList<>();
        // add those nodes with indegree == 0
        for (DirectedGraphNode node : graph)   {
            if (indegreeMap.get(node) == 0) {
                startNodeList.add(node);
            }
        }                  
        return startNodeList;
    }

    private ArrayList<DirectedGraphNode> sortBFS(ArrayList<DirectedGraphNode> startNodeList, 
            Map<DirectedGraphNode, Integer> indegreeMap) {
        ArrayList<DirectedGraphNode> order = new ArrayList<>();       

        Queue<DirectedGraphNode> queue = new LinkedList<>();
        // Because all the nodes in the startList has indegree == 0, 
        // we add them all first
        for (DirectedGraphNode node : startNodeList) {
            queue.offer(node);
            order.add(node);
        }

        while (!queue.isEmpty()) {
            DirectedGraphNode node = queue.poll();
            // each time, we take a node out of the queue, its neighbor's indegree
            // is decremented by 1
            // after the decrement, we add the new nodes with indegree with 0
            for (DirectedGraphNode neighbor : node.neighbors) {
                indegreeMap.put(neighbor, indegreeMap.get(neighbor) - 1);
                if(indegreeMap.get(neighbor) == 0) {
                    queue.offer(neighbor);
                    order.add(neighbor);
                }
            }
        }
        return order;
    }
}
