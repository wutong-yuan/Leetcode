# Lintcode 618 · Search Graph Nodes

# Lintcode **# 618 · Search Graph Nodes **
**
**
**https://www.jiuzhang.com/solutions/search-graph-nodes/**** **
/**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */

public class Solution {
    /*
     * @param graph: a list of Undirected graph node
     * @param values: a hash mapping, <UndirectedGraphNode, (int)value>
     * @param node: an Undirected graph node
     * @param target: An integer
     * @return: a node
     */
    public UndirectedGraphNode searchNode(ArrayList<UndirectedGraphNode> graph,
                                          Map<UndirectedGraphNode, Integer> values,
                                          UndirectedGraphNode node,
                                          int target) {
        // write your code here
        if (node == null) return null;

        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Set<UndirectedGraphNode> set = new HashSet<>();

        queue.offer(node);
        set.add(node);

        while (!queue.isEmpty()) {
            UndirectedGraphNode current = queue.poll();
            if(values.get(current) == target) {
                return current;
            }
            for (UndirectedGraphNode neighbor : current.neighbors) {
                if (set.contains(neighbor)) continue;
                set.add(neighbor);
                queue.offer(neighbor);
            }
        }
        return null;
    }
}
