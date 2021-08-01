# 96. Unique Binary Search Trees

**# 96. Unique Binary Search Trees**# 

# 

https://www.youtube.com/watch?v=Ox0TenN3Zpg 
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        
        
        for (int numberOfNode = 2; numberOfNode <= n; numberOfNode++) {
            int total = 0;
            for (int root = 1; root <= numberOfNode; root++ ) {
                int left = root - 1;
                int right = numberOfNode - root;
                total += dp[left] * dp[right];
            }
            dp[numberOfNode] = total;
        }
        
        return dp[n];
    }
}
