# 64. Minimum Path Sum

**# 64. Minimum Path Sum**

Idea comes from this video
https://www.youtube.com/watch?v=t1shZ8_s6jc 

But this can be improved with O(1) space as below:

class Solution {
    public int minPathSum(int[][] grid) {
        int n = grid.length;
        int m = grid[0].length;
        
        //fill the first row
        for (int i = 1; i < m; i++) {
            grid[0][i] = grid[0][i - 1] + grid[0][i];
        }
        
        //fill out the first column
        for (int j = 1; j < n; j++) {
            grid[j][0] = grid[j - 1][0] + grid[j][0];
        }
        
        // fill out the inner cells
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                grid[i][j] = Math.min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j];
            }
        }
        
        return grid[n - 1][m - 1];       
    }
}

Code can be improved as well :

   int m = grid.length, n = grid[0].length;
    for(int i = 1; i < m; ++i) grid[i][0] += grid[i - 1][0];
    for(int j = 1; j < n; ++j) grid[0][j] += grid[0][j - 1];
    
    for(int i = 1; i < m; ++i){
        for(int j = 1; j < n; ++j){
            grid[i][j] += Math.min(grid[i-1][j], grid[i][j-1]);
        }
    }
    return grid[m-1][n-1];
