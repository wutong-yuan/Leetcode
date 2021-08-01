# 72. Edit Distance

# 72. **# Edit Distance**# 

https://www.youtube.com/watch?v=XYi2-LPrwm4 

class Solution {
    public int minDistance(String word1, String word2) {
        // word1 = abd, word2 = acd
        int n1 = word1.length();
        int n2 = word2.length();
        
        int[][] dp = new int[n1 + 1][n2 + 1];
        
        // fill out the rightmost column
        // 3-2-1-0
        for (int i = 0; i < n1 + 1; i++) {
            dp[i][n2] = n1 - i;
        }
        // fill out the bottom row
        // 3-2-1-0
        for (int j = 0; j < n2 + 1; j++) {
            dp[n1][j] = n2 - j;
        }
        
        for (int i = n1 - 1; i >= 0; i--) {
            for (int j = n2 - 1; j >= 0; j--) {
                if (word1.charAt(i) == word2.charAt(j)) {
                    dp[i][j] = dp[i + 1][j + 1];
                } else {
                    dp[i][j] = 1 + Math.min(Math.min(dp[i][j + 1], dp[i + 1][j]), 
                                            dp[i + 1][j + 1]);
                }
            }
        }
        
        return dp[0][0];
        
    }
}
