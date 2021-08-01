# 300. Longest Increasing Subsequence

**# 300. Longest Increasing Subsequence**

https://www.youtube.com/watch?v=cjWnW0hdF1Y

class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            dp[i] = 1;
        }
        
        for (int i = nums.length - 2; i >= 0; i-- ) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] < nums[j]) {
                    dp[i] = Math.max(dp[i], 1 + dp[j]);
                }
            }
        }
        int longest = 0;
        for (int num : dp) {
            longest = Math.max(longest, num);
        }
        return longest;
    }
}

