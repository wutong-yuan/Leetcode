# 70 Climbing Stairs

# 70 **# Climbing Stairs**

**_DP with memorization_**

class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        
        return findPath(dp, n);
    }
    
    private int findPath(int[] dp, int n) {
        if (n == 1 || n == 0) return 1;
        if (dp[n] != 0) return dp[n];
        
        return dp[n] = findPath(dp, n - 1) + findPath(dp, n - 2);
    }
} 

class Solution {
    public int climbStairs(int n) {
        
        int[] memo = new int[n+1];
        
        for (int i = 0; i < memo.length; i++) {
            memo[i] = Integer.MIN_VALUE;
        }  
        return climbStairs(n, memo);
    }
    
    public static int climbStairs(int n, int[] memo) {
        if (memo[n] > 0)
            return memo[n];
        if(n == 0) {
            return 0;
        }
        if( n == 1) {
            return 1;
        }

        if(n == 2)
            return 2;
        int choices = Integer.MIN_VALUE;
        for (int i = 0; i <= n; i++) {
        choices = Math.max(choices, climbStairs(n - 1, memo) + climbStairs(n - 2, memo));
        }
        memo[n] = choices;
        return choices;
    
    }
    
    
}

