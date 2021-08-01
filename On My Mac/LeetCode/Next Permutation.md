# Next Permutation

1. Next Permutation

https://www.youtube.com/watch?v=LuLCLgMElus 

class Solution {
    public void nextPermutation(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return;
        }
**        // try to find out the breakpoint.It can exist from the second largest index**
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
**        //After we find the breakpoint, we try to find the closest number that is greater than nums[i]. Then we swap nums[i] and nums[j]**
        if(i >= 0) {
            int j = nums.length - 1;
            while(nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1, nums.length - 1);
    }    
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public void reverse(int[] nums, int i, int j) {
        while (i < j) {
            swap(nums, i, j);
                i++;
                j--;
        } 
    }
}

![Next Permutation](images/Next%20Permutation.png)

My code is below:

class Solution {
    public void nextPermutation(int[] nums) {
        if(nums == null || nums.length <= 1) {
            return;
        }
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
        
        if(i >= 0) {
            int j = 0;
            for (j = nums.length - 1; j >= i; j--) {
                if (nums[i] < nums[j]) {
                    break;
                }
            }
            swap(nums, i, j);
        }
        
        reverse(nums, i + 1, nums.length - 1);       
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public void reverse (int[] nums, int start, int end) {
        while (start < end) {
            swap(nums, start, end);
            start++;
            end--;
        }
    }
}
