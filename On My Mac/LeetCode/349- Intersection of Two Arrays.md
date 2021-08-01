# 349. Intersection of Two Arrays

**# 349. Intersection of Two Arrays**
# 

https://www.jiuzhang.com/problem/intersection-of-two-arrays/  see details for time complexity analysis

https://leetcode.com/problems/intersection-of-two-arrays/discuss/81969/Three-Java-Solutions 

This problem tests if you know all the approaches

**_Approach 1  - use two hashSet_**
**_
_**
**Assume nums1.length < nuums2.length. We may create a set to store the smaller array to save some space**
**
**
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> tempResult = new HashSet<>();
        
        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < nums1.length; i++) {
            set.add(nums1[i]);
        }
        
        for (int j = 0; j < nums2.length; j++) {
            if (set.contains(nums2[j])) {
                tempResult.add(nums2[j]);
            }
        }
        
        int[] result = new int[tempResult.size()];
        int i = 0;
        for (Integer val : tempResult) {
            result[i] = val;
            i++;
        }
        
        return result;
    }
}

**_Approach 2: Use two pointers _**

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> tempResult = new HashSet<>();
        
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        int p1 = 0;
        int p2 = 0;
        int length1 = nums1.length;
        int length2 = nums2.length;
        
        while (p2 < length2 && p1 < length1) {
            if (nums1[p1] < nums2[p2]) {
                p1++;
            } else if (nums1[p1] > nums2[p2]) {
                p2++;
            } else {
                tempResult.add(nums1[p1]);
                p1++;
                p2++;
            }
        }
        
        int[] result = new int[tempResult.size()];
        int i = 0;
        for (Integer val : tempResult) {
            result[i] = val;
            i++;
        }
        
        return result;
    }
}

**_Approach 3: binary search_**
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        Set<Integer> set = new HashSet<>();
        
        for (int i = 0; i < nums1.length; i++) {
            if (binarySearch(nums2, nums1[i])) {
                set.add(nums1[i]);
            }       
        }
        
        int[] result = new int[set.size()];
        int i = 0;
        for (Integer val : set) {
            result[i] = val;
            i++;
        }
        
        return result;
    }
    
    private boolean binarySearch(int[] nums, int target) {
        int n = nums.length;
        int left = 0;
        int right = n - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return true;
            } else if (nums[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return false;        
    }
}

**_Extension:_**

![349- Intersection of Two Arrays](images/349- Intersection%20of%20Two%20Arrays.png)

If the two input arrays are very big and contains a lot of zeros . Then we can come up with a data structure to store the non-zeros. Map<position in the array, val>

