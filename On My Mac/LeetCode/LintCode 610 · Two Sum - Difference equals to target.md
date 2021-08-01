# LintCode 610 · Two Sum - Difference equals to target

**# LintCode 610 · Two Sum - Difference equals to target**

public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: an integer
     * @return: [num1, num2] (num1 < num2)
     */
    public int[] twoSum7(int[] nums, int target) {
        // write your code here
        target = Math.abs(target);
        int j = 1;
        for (int i = 0; i < nums.length; i++) {
            /**_/ the reason that j is the bigger of i + 1 or j is that _**
**_            // if nums[j] - nums[i] < target, we will keep moving j to the right_**
**_            // at some point num[j] - nums[i] >= target _**
**_            // if == , we return the nums[j] and nums[i]_**
**_            // if > , we need to keep j still and move i. _**

             j = Math.max(i + 1, j);
             while (j < nums.length && nums[j] - nums[i] < target) {
                 j++;
             }
             if (j >= nums.length) continue;
             
             if (nums[j] - nums[i] == target) {
                 return new int[] {nums[i], nums[j]};
             }
        }

        return new int[] {-1, -1};
    }
}

