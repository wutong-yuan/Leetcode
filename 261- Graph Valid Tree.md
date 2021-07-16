# 261. Graph Valid Tree

**261. Graph Valid Tree**
**
**
**https://www.jiuzhang.com/solutions/graph-valid-tree/**** **
**
**
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if(n == 0) return false;
        
        if (edges.length != n-1) return false;
        
        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);
        
        
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> hash = new HashSet<>();
        
        queue.offer(0);
        hash.add(0);
        
        while(!queue.isEmpty()) {
            int vertice = queue.poll();
            for (int neighbor : graph.get(vertice)) {
                if (hash.contains(neighbor)) continue;
                hash.add(neighbor);
                queue.offer(neighbor);
            }
        }
        if(hash.size() == n) return true;
        return false;      
    }
    
    public Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        //add the nodes first
        for (int i = 0; i < n; i++) {
            // add the node and create an empty set as a set for its neighbors
            graph.put(i, new HashSet<Integer>());
        }
        
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            //add v to u's neighbor set
            graph.get(u).add(v);
            //add u t v's neighbor set
            graph.get(v).add(u);
        }
        
        return graph;
    }
    
    
} 
