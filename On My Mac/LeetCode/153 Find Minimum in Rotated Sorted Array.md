# 153 Find Minimum in Rotated Sorted Array

# 153 **# Find Minimum in Rotated Sorted Array**# 

class Solution {
    public int findMin(int[] nums) {
        int start = 0;
        int end = nums.length - 1;
        int middle = 0;
        while (start < end) {
            middle = start + (end - start) / 2;
            if (nums[middle] > nums[end]) {
                start = middle + 1;
            } else if (nums[middle] < nums[end]) {
                end = middle;
            } 
        }
        // At this point, start = end
        return nums[end];
    } 
} 

**_Use Jiuzhang template_**

class Solution {
    public int findMin(int[] nums) {
        
        int start = 0;
        int end = nums.length - 1;
        if (nums[start] < nums[end]) {
            return nums[start];
        }
        while(start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(nums[start] < nums[mid]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        return Math.min(nums[start], nums[end]);  
    }
}
