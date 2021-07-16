# 55. Jump Game

**55. Jump Game **
**
**
**
**
**https://www.youtube.com/watch?v=muDPTDrpS28**** **
**
**
**
**
class Solution {
    public boolean canJump(int[] nums) {
**        if(nums[0] == 0 && nums.length > 1) return false; // not necessary**
        int reachable = 0;
        int n = nums.length;
        
        for (int i = 0; i < n; i++ ) {
            if(reachable < i) {
                return false;
            }
            reachable = Math.max(nums[i] + i, reachable);
        }
        return true;
    }
}**
**
**
**
**
**
class Solution {

    public boolean canJump(int[] nums) {
    
        int lastPosition = nums.length - 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            if(i + nums[i] >= lastPosition) {
                lastPosition = i;
            }                  
        }
                return lastPosition == 0;

    }
}**
**
