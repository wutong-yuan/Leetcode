# 62. Unique Paths

**62. Unique Paths**
**
**
**Very similar to 64**
** DP:**
**
**
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        
        return findPath(dp, 0, 0, m, n);
    }
    
    private int findPath(int[][] dp, int row, int col, int m, int n) {
        if (row == m -1 && col == n -1) return 1;
        if (dp[row][col] != 0) return dp[row][col];
        if (row == m - 1) return dp[row][col] = findPath(dp, row, col + 1, m, n);
        if (col == n - 1) return dp[row][col] = findPath(dp, row + 1, col, m, n);
        
        return dp[row][col] = findPath(dp, row + 1, col, m, n) + findPath(dp, row, col + 1, m, n);
    }**
**
**} **
**
**
**
**
**Brute force recursive **
**
**
**_Bottom up:_**
**class Solution {**
**    public int uniquePaths(int m, int n) {**
**        if ( m == 1 && n == 1) {**
**            return 1;**
**        }**
**        if (m < 1 || n < 1) {**
**            return 0;**
**        }**
**        **
**        return uniquePaths(m - 1, n) + uniquePaths(m, n - 1);            **
**    }**
**}**
**
**
**
**
**_Top down _****
**
class Solution {

    public static void main(String[] args) {
        int m = 3;
        int n = 7;

        System.*out*.println(*uniquePaths*(0,0,m,n));
    }
    public static int uniquePaths(int i, int j, int m, int n) {
        if (i >= m  || j >= n ) {
            return 0;
        }
        if (i == m - 1 && j == n - 1) {
            return 1;
        }

        return *uniquePaths*(i, j + 1, m, n) + *uniquePaths*(i + 1, j, m, n);
    }
}

**_Dynamic programming_**
class Solution {
    public static void main(String[] args) {
        System.*out*.println(*uniquePaths*(23, 12));
    }

    public static int dpPath(int m, int n, int[][] dp) {
        if (m == 1 || n == 1) {
            return 1;
        }
        if(dp[m][n] != -1) {
            return dp[m][n];
        }
        return dp[m][n] = *uniquePaths*(m - 1, n) + *uniquePaths*(m, n - 1);
    }

    public static int uniquePaths(int m, int n) {
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                dp[i][j] = -1;
            }
        }
        return *dpPath*(m, n, dp);
    }
}

**_Dynamic programming - with no recursive_**
**_
_**
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                dp[i][j] = 1;
            }
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        
        return dp[m - 1][n - 1];
    }
}

**_Math: combinations_**
**_
_**
class Solution {
    public int uniquePaths(int m, int n) {
        int N = m + n - 2;
        int r = n - 1;
**_        double result = 1; // Be careful about this. _**
        
        for (int i = 1; i <= n - 1; i++) {
            result = result * (N - r + i) / i;
        }
        
        return (int)result;
    }
}

https://www.youtube.com/watch?v=t_f0nwwdg5o&list=PLgUwDviBIf0rPG3Ictpu74YWBQ1CaBkm2&index=18 
**_
_**
**_
_**

