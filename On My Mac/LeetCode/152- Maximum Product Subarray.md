# 152. Maximum Product Subarray

**# 152. Maximum Product Subarray**
**
**
**See paper notes to see dry run **

class Solution {
    public int maxProduct(int[] nums) {
        
        int n = nums.length;
        int maxSoFar = nums[0];
        int minSoFar = nums[0];
        int max = nums[0];
        
        for (int i = 1; i < n; i++) {
            int current = nums[i];
            int tempMax = Math.max(current, 
                                Math.max(current * maxSoFar, current * minSoFar));
            minSoFar = Math.min(current, 
                                Math.min(current * maxSoFar, current * minSoFar));
            maxSoFar = tempMax;
            max = Math.max(maxSoFar, max);
        }
        return max;
    }
}

