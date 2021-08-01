# LintCode 461 · Kth Smallest Numbers in Unsorted Array

# LintCode **# 461 · Kth Smallest Numbers in Unsorted Array**

public class Solution {
    /**
     * @param k: An integer
     * @param nums: An integer array
     * @return: kth smallest element
     */
    public int kthSmallest(int k, int[] nums) {
        // write your code here

        return quickSort(k, nums, 0, nums.length - 1);
    }

    private int quickSort(int k, int[] nums, int start, int end) {
        if (start <= end) {
            int p = partition(nums, start, end);
            if **_(p == k - 1) _**{ // be careful here, it is k -1 not k
                return nums[p];
            } 
            if (p > k - 1) {
                return quickSort(k, nums, start, p - 1);
            }
            return quickSort(k, nums, p + 1, end);
        }
        return -1;
    }

    private int partition(int[] nums, int start, int end) {
        int pivot = end;
        int p = start;
        for (int i = start; i < end; i++) {
            if (nums[i] <= nums[pivot]) {
                swap(nums, i, p);
                p++;
            }
        }
        swap(nums, p, pivot);

        return p;
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
