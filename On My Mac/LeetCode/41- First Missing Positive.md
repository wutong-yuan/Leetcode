# 41. First Missing Positive

**41. First Missing Positive **
**
**
**
**
**https://leetcode.com/problems/first-missing-positive/discuss/319270/Explanation-of-crucial-observation-needed-to-deduce-algorithm**** **
**
**
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if(nums[i] <= 0 || nums[i] > n) {
                nums[i] = n + 1;
            }
        }
        
        for (int i = 0; i < n; i++) {
            int temp = Math.abs(nums[i]);
            if (temp > n) {
                continue;
            }
            
            temp--;
**            if(nums[temp] > 0) { // we need this check. Please check paper notes to see why**
                nums[temp] *= -1;
            }
        }
        
        for (int i = 0; i < n; i++) {
            if(nums[i] > 0) {
                return i + 1;
            }
        }
        return n + 1;
    }
}

