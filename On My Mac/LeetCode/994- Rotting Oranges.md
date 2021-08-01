# 994. Rotting Oranges

**# 994. Rotting Oranges**

https://www.jiuzhang.com/solutions/zombie-in-matrix/ 

class Coordinate {
    int x;
    int y;
    public Coordinate(int x ,int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    
    public int empty = 0;
    public int fresh = 1;
    public int rotten = 2;
    
    public int[] directionX = {0, 1, -1, 0};
    public int[] directionY = {1, 0, 0, -1};
    
    public int orangesRotting(int[][] grid) {
        
        int rows = grid.length;
        int cols = grid[0].length;
        int numOfFresh = 0;
        int minutes = 0;
        
        Queue<Coordinate> queue = new LinkedList<>();
        
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == rotten) {
                    queue.offer(new Coordinate(i, j));
                }
                if(grid[i][j] == fresh) {
                    numOfFresh++;
                }
            }
        }
        
        if (numOfFresh == 0) return 0;
        
        while (!queue.isEmpty()) {
            minutes++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Coordinate coor = queue.poll();
                for (int j = 0; j < directionX.length; j++) {
                    Coordinate adj = new Coordinate(coor.x + directionX[j],
                                                   coor.y + directionY[j]);
                    if (inBound(adj, grid)) {
                        if(grid[adj.x][adj.y] == fresh) {
                            grid[adj.x][adj.y] = rotten;
                            numOfFresh--;
                            if(numOfFresh == 0) {
                                return minutes;
                            }
                            queue.offer(adj);
                        }
                    }
                }
            }        
        }
        
        return -1;
    }
    
    private boolean inBound(Coordinate coor, int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        if (coor.x < 0 || coor.x >= rows || 
           coor.y < 0 || coor.y >= cols) {
            return false;
        }
        return true;
    }
}
