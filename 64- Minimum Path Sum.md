# 64. Minimum Path Sum

**# 64. Minimum Path Sum**
# 

**_DP with memoization  Top down_**
class Solution {
    public int minPathSum(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        int[][] dp = new int[rows][cols];
        return findPath(grid, dp, 0, 0);
    }
    
    private int findPath(int[][] grid, int[][] dp, int row, int col) {
        int m = grid.length;
        int n = grid[0].length;
        if(dp[row][col] != 0) {
            return dp[row][col];
        }
        
        if (row == m - 1 && col == n - 1) {
            dp[row][col] = grid[row][col];
        } else if (row == m -1) {
            dp[row][col] = grid[row][col] + findPath(grid, dp, row, col + 1);
        } else if (col == n -1) {
            dp[row][col] = grid[row][col] + findPath(grid, dp, row + 1, col);
        } else {
            dp[row][col] = grid[row][col] + Math.min(findPath(grid, dp, row + 1, col), 
                                                    findPath(grid, dp, row, col + 1));
        }
        return dp[row][col];
    }
}

**_DP with memoization  Bottom up_**
**_
_**
class Solution {
    public int minPathSum(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        int[][] dp = new int[rows][cols];
        return findPath(grid, dp, rows - 1, cols - 1);
    }
    
    private int findPath(int[][] grid, int[][] dp, int row, int col) {
        int m = grid.length;
        int n = grid[0].length;
        if(dp[row][col] != 0) {
            return dp[row][col];
        }
        
        if (row == 0 && col == 0) {
            dp[row][col] = grid[row][col];
        } else if (row == 0) {
            dp[row][col] = grid[row][col] + findPath(grid, dp, row, col - 1);
        } else if (col == 0) {
            dp[row][col] = grid[row][col] + findPath(grid, dp, row - 1, col);
        } else {
            dp[row][col] = grid[row][col] + Math.min(findPath(grid, dp, row - 1, col), 
                                                    findPath(grid, dp, row, col - 1));
        }
        return dp[row][col];
    }
}

**_In pace _**

class Solution {
    public int minPathSum(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        for (int r = 1; r < rows; r++) {
            grid[r][0] = grid[r -1][0] + grid[r][0];
        }
        
        for (int c = 1; c < cols; c++) {
            grid[0][c] = grid[0][c - 1] + grid[0][c];
        }
        
        for (int r = 1; r < rows; r++) {
            for (int c = 1; c < cols; c++) {
                grid[r][c] = Math.min(grid[r -1][c], grid[r][c -1]) + grid[r][c];
            }
        }
        
        return grid[rows - 1][cols - 1];
    }
}
