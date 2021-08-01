# 63. Unique Paths II

**# 63. Unique Paths II**
# 

The idea comes from the video below.
https://www.youtube.com/watch?v=z6kelCB0ww4 

Code below is more concise.
https://leetcode.com/problems/unique-paths-ii/discuss/23250/Short-JAVA-solution 

public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    int width = obstacleGrid[0].length;
    int[] dp = new int[width];
    dp[0] = 1; /**/ for the first cell. It is always 1. There is one way to reach the first cell**

    for (int[] row : obstacleGrid) {
        for (int j = 0; j < width; j++) {
            if (row[j] == 1)
                dp[j] = 0;
            else if (j > 0) // we skip j = 0 because for the first row and first column, there is only one way to reach the end of the first row and column. If there is no obstacle, the first row will be 1,1,1,…., and the first column will be 1,1,1,…. If there is obstacle in the middle, please see table below.
                dp[j] += dp[j - 1]; /**/ here dp[j] = dp[j] + dp[j - 1]. dp[j] comes from the last row, which is the top cell and dp[j -1] was updated before dp[j], which is the left cell. It is always updated before dp[j]. **
        }
    }
    return dp[width - 1];
}

No obstacle
Original grid:
|  0<br/> | 0<br/> | 0<br/> |
|-----|-----|-----|
|  0<br/> |  |  |
|  0<br/> |  |  |

dp: 
|  1<br/> | 1<br/> | 1<br/> |
|-----|-----|-----|
|  1<br/> |  |  |
|  1<br/> |  |  |

With obstacle
Original grid:
|  0<br/> | 1<br/> | 0<br/> |
|-----|-----|-----|
|  1<br/> |  |  |
|  0<br/> |  |  |

dp: within the first row or column, if there is one obstacle, anything after that will be always 0
|  1<br/> | 0<br/> | 0<br/> |
|-----|-----|-----|
|  0<br/> |  |  |
|  0<br/> |  |  |

**_DP + memorization _**

class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int rows = obstacleGrid.length;
        int cols = obstacleGrid[0].length;
        int[][] dp = new int[rows][cols];
        
        return findPath(dp, obstacleGrid, 0, 0, rows, cols);
    }
    
    public int findPath(int[][] dp, 
                        int[][] obstacleGrid, 
                        int r, 
                        int c,
                        int rows, 
                        int cols ) {
        if (obstacleGrid[r][c] == 1) return 0;
        if (r == rows - 1 && c == cols - 1) {
            return 1;
        }
        if (dp[r][c] != 0) return dp[r][c];
        
        if (r == rows - 1) return findPath(dp, obstacleGrid, r, c + 1, rows, cols);
        if (c == cols - 1) return findPath(dp, obstacleGrid, r + 1, c, rows, cols);
        
        return dp[r][c] = findPath(dp, obstacleGrid, r + 1, c, rows, cols) +
                            findPath(dp, obstacleGrid, r, c + 1, rows, cols);
        
    }
}
