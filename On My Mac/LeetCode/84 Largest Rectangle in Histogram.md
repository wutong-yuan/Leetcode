# 84 Largest Rectangle in Histogram

# 84**#  Largest Rectangle in Histogram**

https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28902/5ms-O(n)-Java-solution-explained-(beats-96) 
Above is the faster approach

Below is the one using stack
https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28900/Short-and-Clean-O(n)-stack-based-JAVA-solution 

public int largestRectangleArea(int[] heights) {
        int len = heights.length;
        int maxArea = 0;
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i <= len;) {
            int h = (i == len ? 0 : heights[i]);
            if (stack.isEmpty() || h >= heights[stack.peek()]) {
                stack.push(i);
                i++;
            }else {
                int curHeight = heights[stack.pop()];
                int rightBoundary = i - 1;
                int leftBoundary = stack.isEmpty() ? 0 : stack.peek() + 1;
                int width = rightBoundary - leftBoundary + 1;
                maxArea = Math.max(maxArea, (curHeight * width));
            }
        }
        return maxArea;
    }
 
**_With explanation _**
class Solution {
    public int largestRectangleArea(int[] heights) {
        // example {2,1,5,6,2,3}
        Stack<Integer> stack = new Stack<>();
        int n = heights.length;
        
        int max = 0;
        // i == n in order to find the right bound for the last position
        for (int i = 0; i <= n;) {
            int height = (i == n ? 0 : heights[i]);
            // we just keep pushing i into the stack as long as the height is
            // increasing until we see the new height
            // is smaller than the peek index's height. This means, we see
            // the right bound for a couple of positions. That is when we calculate the area.
            // Example: we push position 0 into the stack, then we see position 1, h[1] < h[0],
            // we need to stop and calcualte the area for postion 0 becasue we see the right bound.
            // at the same time we pop the previous postion out becasue it is done.
            // Example : then we push position 1 into the stack, then we see position 2(h[2] = 5 h[1]), 
            // we continue to push i into the stack until we see position 4. Then we found the right bound
            // for position 2 and 3. Then we calcualte the area for those two by popping them out. becaue
            // they are done.
            // we pop can calculate until we see the peek index's heght is smaller than the current position 
            // like h[1] = 1 < h[4] (2), we keep 1 in the stack because we haven't found the right bound for
            // it yet. 
            // below while loop will continue to be executed until the peek element's height is lower than
            // i's height
            if (stack.isEmpty() || heights[stack.peek()] <= height) {
                stack.push(i);
                i++;
            } else {
                
                int currHeight = heights[stack.pop()];
                int leftBound = -1;
                if (!stack.isEmpty() ) {
                    leftBound = stack.peek();
                }
                // the index before the current i is the right bound
                int rightBound = i - 1;
                int area = (rightBound - leftBound) * currHeight;
                max = Math.max(area, max);
            }

        }
        return max;
            
    }
}

![84 Largest Rectangle in Histogram](images/84 Largest%20Rectangle%20in%20Histogram.png)

