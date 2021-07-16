# 4 Median of Two Sorted Arrays

# 4**#  Median of Two Sorted Arrays**

https://www.youtube.com/watch?v=LPFhl65R7ww&t=387s 

 class Solution {
    
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        
        int x = nums1.length;
        int y = nums2.length;
        double result = 0;
        
        if (x > y) {
            return findMedianSortedArrays(nums2, nums1);
        }
        int low = 0;
        int high = x;
        
        while (low <= high) {
            int partitionX = (low + high) / 2;
            int partitionY = (x + y + 1) / 2 - partitionX;
            
            int maxLeftX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
            int minRightX = (partitionY == x) ? Integer.MAX_VALUE : nums1[partitionX];
            
            int maxLeftY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
            int minRightY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];
            
            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                if((x + y) % 2 == 0) {
                   result = (double)(Math.max(maxLeftX, maxLeftY) + Math.min(minRightX, minRightY)) / 2;
                    break;
                }else {
                    result = (double)Math.max(maxLeftX, maxLeftY);
                    break;
                }     
            } else if (maxLeftX > minRightY ) {
                high = partitionX - 1;
            } else if (maxLeftY > minRightX) {
                low = partitionX + 1;
            }
        }
        return result;
    }
}
