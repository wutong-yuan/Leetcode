# 200. Number of Islands

**# 200. Number of Islands **

https://www.youtube.com/watch?v=__98uL6wst8 
Algorithm comes from this video

class Coordinate {
    int x;
    int y;
    
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Solution {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        int numOfRows = grid.length;
        int numOfColumns = grid[0].length;
        int numOfIslands = 0;
        
        for (int i = 0; i < numOfRows; i++) {
            for (int j = 0; j < numOfColumns; j++) {
                if (grid[i][j] == '1') {
                    markAdjCells(grid, i, j);
                    numOfIslands++;
                }
            }
        }
        return numOfIslands;
    }
    
    private void markAdjCells(char[][] grid, int x, int y) {
        
        int[] directionX = {0, 1, -1, 0};
        int[] directionY = {1, 0, 0, -1};
        
        Queue<Coordinate> queue = new LinkedList<>();       
        queue.offer(new Coordinate(x, y));
        grid[x][y] = '0';
        
        while (!queue.isEmpty()) {
            Coordinate coor = queue.poll();
            for (int i = 0; i < directionX.length; i++) {
                Coordinate adjacent = new Coordinate(coor.x + directionX[i], 
                                                    coor.y + directionY[i]);
                if (inBound(grid, adjacent.x, adjacent.y)) {
                    if (grid[adjacent.x][adjacent.y] == '1') {
                        grid[adjacent.x][adjacent.y] = '0';
                        queue.offer(adjacent);
                    }
                }
                
            }
        }
    }
    
    private boolean inBound (char[][] grid, int x, int y) {
        int numOfRows = grid.length;
        int numOfCol = grid[0].length;
        
        if (x > numOfRows - 1 || x < 0 ||
           y > numOfCol - 1 || y < 0) {
            return false;
        }
        
        return true;
    }
    
}
