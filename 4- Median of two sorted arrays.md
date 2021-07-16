# 4. Median of two sorted arrays

 4. Median of two sorted arrays

My solution:

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        double median = Integer.MAX_VALUE;
        int[] combinedNum = new int[nums1.length + nums2.length];
        int combinedLength = combinedNum.length;
        for (int i = 0; i < nums1.length; i++) {
            combinedNum[i] = nums1[i];
        }
        
        for (int j = 0; j < nums2.length; j++) {
            combinedNum[nums1.length + j] = nums2[j];
        }
        
        Arrays.sort(combinedNum);
        
        if(combinedLength % 2 != 0) {
            int medianPostion = combinedLength / 2;
            median = combinedNum[medianPostion];
        } else {
            int tempPosition1 = combinedLength / 2 - 1;
            int tempPosition2 = combinedLength / 2;
            median = ((double)(combinedNum[tempPosition1] + combinedNum[tempPosition2])) / 2;
        }        
        return median;
    }
}

