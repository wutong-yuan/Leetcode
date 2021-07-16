# 42. Trapping Rain Water

**42. Trapping Rain Water **

https://www.youtube.com/watch?v=ZI2z5pq0TqA 

**Be careful:**
**See paper notes first.**

class Solution {
    public int trap(int[] height) {
        if(height.length == 0 || height == null) {
            return 0;
        }
        int l = 0;
        int r = height.length - 1;
        int result = 0;
        int maxL = height[l];
        int maxR = height[r];
        
        while (l < r) {

           if(maxL <= maxR) {
               l++;
               maxL = Math.max(maxL, height[l]);
               result += maxL - height[l];
           } else {
               r--;
               maxR = Math.max(maxR, height[r]);
               result += maxR - height[r];
           }
            
        }
        return result;
    }
}

