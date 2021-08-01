# LintCode 31 · Partition Array

# LintCode **# 31 · Partition Array**
**
**
public class Solution {
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        if (nums == null || nums.length == 0) return 0;
        // write your code here
        int left = 0;
        int right = nums.length - 1;

        while (left < right) {
            while (left < right && nums[left] < k ) {
                left++;
            }
**// be careful about the equal sign below.= means if the element equals to k, we partition it to the right side**
            while (left < right && nums[right] >**= **k) {
                right--;
            }

            if (left < right) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
**                left++;**
**                right--;**
**// Be careful here, don’t forget**

            }
        }
        if (nums[left] < k) {
            return left + 1;
        }
        return left;
    }
}

