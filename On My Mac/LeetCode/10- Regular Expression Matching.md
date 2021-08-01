# 10. Regular Expression Matching

**# 10. Regular Expression Matching**

**# https://www.youtube.com/watch?v=HAA8mgxlov8****#  **# 

class Solution {
    int match = 1;
    int nMatch = 2;
    public boolean isMatch(String s, String p) {
        int sLen = s.length();
        int pLen = p.length();
        int[][] dp = new int[sLen + 1][pLen + 1];
        int result = dfs(s, p, 0, 0, dp);
        
        return result == match;
    }
    
    private int dfs (String s, String p, int pointerS, int pointerP, int[][] dp) {
        if (pointerS >= s.length() && pointerP >= p.length()) {
            return match;
        }
        // we still have something in the s but p is out of bound.
        if (pointerP >= p.length()) return nMatch;
        
        if (dp[pointerS][pointerP] != 0) 
            return dp[pointerS][pointerP];
        
        boolean isMatch = (pointerS < s.length() &&
                         (s.charAt(pointerS) == p.charAt(pointerP) ||
                         p.charAt(pointerP) == '.'));
        if (pointerP < p.length() - 1 && p.charAt(pointerP + 1) == '*') {
            if (dfs(s, p, pointerS, pointerP + 2, dp) == match ||
               (isMatch && dfs(s, p, pointerS + 1, pointerP, dp) == match)) {
                return dp[pointerS][pointerP] = match;
            }
        }
        if (isMatch) {
             return dp[pointerS][pointerP] = dfs(s, p, pointerS + 1, pointerP + 1, dp);
        }
        
        return nMatch;
    }
}

![10- Regular Expression Matching](images/10- Regular%20Expression%20Matching.png)

