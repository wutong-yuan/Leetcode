# 97. Interleaving String

**# 97. Interleaving String**
# 

https://www.youtube.com/watch?v=3Rw3p9LrgvE 

class Solution {
    int match = 1;
    int notMatch = 2;
    int unknown = 0;
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        int[][] dp = new int[s1.length() + 1][s2.length() + 1];
        
        return dpHelper(s1, s2, s3, 0, 0, dp);
    }
    
    private boolean dpHelper(String s1, String s2, String s3, int i, int j, int[][] dp) {
        if (i == s1.length() && j == s2.length()) {
            dp[i][j] = match;
            return true;
        }
        
        if (dp[i][j] != unknown) {
            return dp[i][j] == match ? true : false;
        }
        
        if (i < s1.length() && s1.charAt(i) == s3.charAt(i + j) &&
                                dpHelper(s1, s2, s3, i + 1, j, dp)) {
            dp[i][j] = match;
            return true;
        }
        
        if (j < s2.length() && s2.charAt(j) == s3.charAt(i + j) &&
                                dpHelper(s1, s2, s3, i, j + 1, dp)) {
            dp[i][j] = match;
            return true;
        }
        
        dp[i][j] = notMatch;
        return false;
    }
}

**_DP approach_**

class Solution {

    public boolean isInterleave(String s1, String s2, String s3) {
        int n1 = s1.length();
        int n2 = s2.length();
        int n3 = s3.length();
        
        if (n1 + n2 != n3) {
            return false;
        }  
        
        boolean[][] dp = new boolean[n1 + 1][n2 + 1];
        dp[n1][n2] = true;
        
        for (int i = n1; i >= 0; i--) {
            for (int j = n2; j >= 0; j--) {
                if(i < n1 && s1.charAt(i) == s3.charAt(i + j) && dp[i + 1][j]) {
                    dp[i][j] = true;   
                }
                if (j < n2 && s2.charAt(j) == s3.charAt(i + j) && dp[i][j + 1]) {
                    dp[i][j] = true;
                }
            }
        }
        return dp[0][0];
    }
}
