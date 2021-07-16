# 34. Find First and Last Position of Element in Sorted Array

**34. Find First and Last Position of Element in Sorted Array **

https://www.youtube.com/watch?v=dVXy6hmE_0U&t=306s 
![34- Find First and Last Position of Element in Sorted Array](images/34- Find%20First%20and%20Last%20Position%20of%20Element%20in%20Sorted%20Array.png)

class Solution {
    // the main idea is to find the first postion that is greater or equal to the target --> firstPosition. Then find the first postion that is greater or equal to the target + 1. Anything in between is our target range
    public int[] searchRange(int[] nums, int target) {
        int firstPostion = firstPosition(nums, target);
        int secondPostion = firstPosition(nums, target + 1) - 1;
        
        if (firstPostion <= secondPostion) {
            return new int[] {firstPostion, secondPostion};
        } else {
            return new int[] {-1, -1};
        }
    }
    
    public int firstPosition(int[] nums, int target) {
        //find the first position that is greater or equal to target
        int n = nums.length;
        int left = 0;
        int right = n - 1;
        int firstPosition = n;
        while (left <= right) {
            int middle = left + (right - left) / 2;
            if (nums[middle] >= target) {
                // if the middle element is greater or equal to target, probably the middle postion
                // is the first postion that is greater or equal to target. But it is also posstible 
                // that it is not the first. For example, 5,7,7,8,8,8,8,8,9 and target is 8.
                // obviously the first middle, 8 is not the first postion. So in this case, we still
                // need to keep looking at the left side and update the first position until it 
                //reaches the real first 
                firstPosition = middle;
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }
        return firstPosition;
    }
}

**_Use Jiuzhang approach_**

class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums == null || nums.length == 0) {
            return new int[] { -1, -1};
        }
        int n = nums.length;
        int start = 0;
        int end = n - 1;        
        // search for the first position
        int firstPosition = findFirst(start, end, nums, target);
        int lastPosition = findLast(start, end, nums, target);
        return new int[] { firstPosition, lastPosition};
    }
    
    public int findFirst(int start, int end, int[] nums, int target) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(nums[mid] == target ||nums[mid] > target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] == target) return start;
        if (nums[end] == target) return end;
        return -1;
    }
    
    public int findLast(int start, int end, int[] nums, int target) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(nums[mid] == target || nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[end] == target) return end;       
        if (nums[start] == target) return start;
        return -1;    
    }
}
