# 323. Number of Connected Components in an Undirected Graph

**# 323. Number of Connected Components in an Undirected Graph **# 

**_My solution based on BFS_**

class Solution {
    public int countComponents(int n, int[][] edges) {
        if (n == 0) return 0;
        
        int components = 0;
        Set<Integer> included = new HashSet<>();
        
        for (int i = 0; i < n; i++) {
            if(!included.contains(i)) {
                Queue<Integer> queue = new LinkedList<>();
                Set<Integer> set = new HashSet<>();
                queue.offer(i);
                set.add(i);
                included.add(i);

                while (!queue.isEmpty()) {
                    int currentNode = queue.poll();
                    for (int[] edge : edges) {
                        int u = edge[0];
                        int v = edge[1];
                        if(u == currentNode && !set.contains(v)) {
                            queue.offer(v);
                            set.add(v);
                            included.add(v);
                        } else if (v == currentNode && !set.contains(u)) {
                            queue.offer(u);
                            set.add(u);
                            included.add(u);
                        }
                    }
                }
             components++;
            }            
        }
        
        return components;      
    }
}
