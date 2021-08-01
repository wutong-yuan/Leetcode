# 74 Binary Search

**_recursion_**
class Solution {
    public int search(int[] nums, int target) {
        return binarySearch(0, nums.length - 1, nums, target);
        
    }
    
    public int binarySearch(int start, int end, int[] nums, int target) {
        if (start > end) {
            return -1;
        }
        int mid = start + (end - start) / 2;
        if(target == nums[mid]) {
            return mid;
        }
        if(target > nums[mid]) {
            return binarySearch(mid + 1, end, nums, target);
        }
        if(target < nums[mid]) {
            return binarySearch(start, mid - 1, nums, target);
        }
        return -1;
    }
}

**_Non-recursion_**
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (target == nums[mid]) return mid;
            if(target > nums[mid]) {
                low =  mid + 1;
            } else {
                high = mid - 1;
            }
        }
**_        return nums[low] == target ? low : -1;      // be careful about this _**
    }
}

