# 115. Distinct Subsequences

**# 115. Distinct Subsequences**
# 

**_Top down dp with memoization _**

class Solution {
    public int numDistinct(String s, String t) {
        int lenS = s.length();
        int lenT = t.length();
        int[][] dp = new int[lenS + 1][lenT + 1];
        for (int i = 0; i < dp.length; i++) {
            for (int j = 0; j < dp[0].length; j++) {
                dp[i][j] = -1;
            }
        }
        
        return dp(s, t, 0, 0, dp);
    }
    
    private int dp(String s, String t, int i, int j, int[][] dp) {
        if (j == t.length()) return 1;
        if (i == s.length()) return 0;
        if (dp[i][j] != -1) return dp[i][j];
        
        if(s.charAt(i) == t.charAt(j)) {
            dp[i][j] = dp(s, t, i + 1, j + 1, dp) +
                        dp(s, t, i + 1, j, dp);
        } else {
            dp[i][j] = dp(s, t, i + 1, j, dp);
        }
        
        return dp[i][j];
        
    }
}

**_Bottom up _**

class Solution {
    public int numDistinct(String s, String t) {
        int sLen = s.length();
        int tLen = t.length();
        int[][] dp = new int[sLen + 1][tLen + 1];
        
        for (int i = 0; i < dp.length; i++) {
            dp[i][tLen] = 1;
        }
        
        for (int j = 0; j < dp[0].length; j++) {
            dp[sLen][j] = 0;
        }
        
        dp[sLen][tLen] = 1;
        
        for (int i = sLen - 1; i >= 0; i--) {
            for (int j = tLen - 1; j >=0; j--) {
                if (s.charAt(i) == t.charAt(j)) {
                    dp[i][j] = dp[i + 1][j + 1] + 
                                dp[i + 1][j];
                } else {
                    dp[i][j] = dp[i + 1][j];
                }
            }
        }
        
        return dp[0][0];
    }
}

![115- Distinct Subsequences](images/115- Distinct%20Subsequences.png)

![115- Distinct Subsequences-1](images/115- Distinct%20Subsequences-1.png)

**_Use less space _**

![115- Distinct Subsequences-2](images/115- Distinct%20Subsequences-2.png)

class Solution {
    public int numDistinct(String s, String t) {
        int sLen = s.length();
        int tLen = t.length();
        
        int[] dp = new int[tLen + 1];
        dp[tLen] = 1;
        
        for (int i = sLen - 1; i >=0; i--) {
            // for each row, the last column is always 1
            int prev = 1;
            for (int j = tLen - 1; j>= 0; j--) {
                // before proceed, need to record the dp[i+1][j+1] for the next loop purpose
                // we don't use this value for this current j
                int rowPlus1ColPlus1DP = dp[j];
                
                if (s.charAt(i) == t.charAt(j)) {
                    // dp[i][j] + dp[i + 1][j + 1], the first prev is always 1
                    dp[j] += prev; 
                }
                
                prev = rowPlus1ColPlus1DP;
            }
        }
        
        return dp[0];
    }
}
