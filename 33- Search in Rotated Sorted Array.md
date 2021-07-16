# 33. Search in Rotated Sorted Array

**33. Search in Rotated Sorted Array**
**
**
![33- Search in Rotated Sorted Array](images/33- Search%20in%20Rotated%20Sorted%20Array.png)

![33- Search in Rotated Sorted Array-1](images/33- Search%20in%20Rotated%20Sorted%20Array-1.png)**
**
**
**
class Solution {
    public int search(int[] nums, int target) {
 **       //find the min - this is OK but not O(lgn)**
**        int i = 0;**
**        while (i < nums.length - 1) {**
**            if(nums[i] < nums[i + 1]) {**
**                i++;**
**            } else {**
**                break;**
**            }**
**        }**

        
        if(target > nums[0]) {
            return binarySearch(nums, 0, i, target);
        } else if (target < nums[0]) {
            return binarySearch(nums, i + 1, nums.length -1, target);
        }else if(target == nums[0]) {
            return 0;
        } 
        return -1;
    }
    
    public int findRotateIndex(intint[] nums, int start, int end) {
        if (nums[start] < nums[end]) {
            return 0;
        }
        
        int middle = start + (end - start) / 2;
        while (start <= end ) {
            if(nums[middle] > nums[middle + 1]) {
                return middle + 1;
            } else {
                if(nums[middle]  < nums[left]) {
                end = middle - 1;
                } else {
                start = middle + 1;
                }
            }
        }       
        return 0;
    }
    
    public int binarySearch(int[] nums, int start, int end, int target) {
        if(start > end) {
            return -1;
        }
        int middle = start + (end - start) / 2;
        if(target < nums[middle] ) {
            return binarySearch(nums, start, middle - 1, target);
        } else if (target > nums[middle]) {
            return binarySearch(nums, middle + 1, end, target);
        } else {
            return middle;
        }
    }
}

**_Jiuzhang approach_**

public class Solution {
    /**
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    public int search(int[] A, int target) {
        // write your code here
        if(A == null || A.length == 0) return -1;
        int n = A.length;
        int start = 0;
        int end = n - 1;

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(A[mid] == target) {
                return mid;
            }
            if (A[mid] > A[start]) {
                if(A[start] <= target && target < A[mid]) {
                    end = mid;
                } else {
                    start = mid;
                }
            }else {
                if (A[mid] < target && target <= A[end] ) {
                    start = mid;
                } else {
                    end = mid;
                }
            }
        }
        if(A[start] == target) return start;
        if(A[end] == target) return end;
        return -1;
    }
}
