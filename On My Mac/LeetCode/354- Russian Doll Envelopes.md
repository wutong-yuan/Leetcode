# 354. Russian Doll Envelopes

**# 354. Russian Doll Envelopes**
# 

https://www.youtube.com/watch?v=3fF1r5nhQX4 

**_Compare to 300. _**
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        int r = envelopes.length;
        int c = envelopes[0].length;
        
        int[] dp = new int[r];
        for (int i = 0; i < r; i++) {
            dp[i] = 1;
        }
        
Arrays.*sort*(envelopes, new Comparator<int[]>() {
    public int compare(int[] a, int[] b) {
        return a[0] - b[0];
    }
});

                
        for (int i = r - 2; i >= 0; i--) {
            for (int j = i + 1; j < r; j++) {
                if (envelopes[j][0] > envelopes[i][0] &&
                   envelopes[j][1] > envelopes[i][1]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < dp.length; i++) {
            max = Math.max(max, dp[i]);
        }
        
        return max;
    }
}
