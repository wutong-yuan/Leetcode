# 209. Minimum Size Subarray Sum

**209. Minimum Size Subarray Sum**
**
**
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int n = nums.length;
        int start = 0;
        int sum = 0;
        int window = Integer.MAX_VALUE;
        
        for (int end = 0; end < n; end++) {
            sum += nums[end];
            while (sum >= target) {
                window = Math.min(window, end - start + 1);
                sum -= nums[start];
                //contract the window
                start++;
            }
        }
        return window == Integer.MAX_VALUE ? 0 : window;
    }
}**
**
**
**
**See paper notes of a real run **
**
**
**May need to consider the binary search approach as well**
