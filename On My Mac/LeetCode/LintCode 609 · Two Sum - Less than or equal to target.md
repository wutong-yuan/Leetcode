# LintCode 609 · Two Sum - Less than or equal to target

# LintCode **# 609 · Two Sum - Less than or equal to target**
**
**
pu

blic class Solution {
    /**
     * @param nums: an array of integer
     * @param target: an integer
     * @return: an integer
     */
    public int twoSum5(int[] nums, int target) {
        // write your code here

        if (nums == null || nums.length < 2) {
            return 0;
        }

        Arrays.sort(nums);
        int left = 0;
        int right = nums.length - 1;
        int count = 0;
        while (left < right) {
            if (nums[left] + nums[right] > target) {
                right--;
            } else {
                count += right - left;
                left++;
            }
        }

        return count;
    }
}
