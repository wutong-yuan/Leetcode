# Container with Most water

1. Container with Most water

My solution:

class Solution {
    public int maxArea(int[] height) {
        int length = height.length;
        int sum = Integer.MIN_VALUE;
        int tempSum = 0;
        for (int i = 0; i < length; i++) {
            for (int j = i; j < length; j++) {
                tempSum = (j - i) * Math.min(height[i], height[j]);
                if (tempSum > sum) {
                    sum = tempSum;
                }
            }
        }
        return sum;       
    }
}

