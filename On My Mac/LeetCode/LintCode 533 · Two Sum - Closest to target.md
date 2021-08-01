# LintCode 533 · Two Sum - Closest to target

# LintCode **# 533 · Two Sum - Closest to target**

public class Solution {
    /**
     * @param nums: an integer array
     * @param target: An integer
     * @return: the difference between the sum and the target
     */
    public int twoSumClosest(int[] nums, int target) {
        // write your code here

        if (nums == null || nums.length < 2) return 0;

        Arrays.sort(nums);
        int left = 0;
        int right = nums.length - 1;
        int minDiff = Integer.MAX_VALUE;

        while (left < right) {
            int sum = nums[left] + nums[right];
            int tempDiff = Math.abs(sum - target);
            if (sum == target) {
                return tempDiff;
            } else if (sum > target) {
                right--;
            } else {
                left++;
            }
            minDiff = Math.min(minDiff, tempDiff);
        }
        return minDiff;
    }
}

