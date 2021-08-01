# 85. Maximal Rectangle

**# 85. Maximal Rectangle**
# 

class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0 || matrix == null) return 0;
        int cols = matrix[0].length;
        int[] heights = new int[cols];
        
        int max = 0;
        for (char[] row : matrix) {
            for (int i = 0; i < cols; i++) {
                heights[i] = (row[i] == '1' ? heights[i] + 1 : 0);
            }
            max = Math.max(max, getArea(heights));
        }
        return max;        
    }
    
    private int getArea(int[] heights) {
        int n = heights.length;
        Stack<Integer> stack = new Stack<>();
        
        int max = 0;
        for (int i = 0; i <= n;) {
           int height = (i == n ? 0 : heights[i]);
            if (stack.isEmpty() || height >= heights[stack.peek()]) {
                stack.push(i);
                i++;
            } else {
                int currHeight = heights[stack.pop()];
                int rightBound = i - 1;
                int leftBound = (stack.isEmpty() ? -1 : stack.peek());
                int width = rightBound - leftBound;
                int area = currHeight * width;
                max = Math.max(max, area);               
            }
        }
        return max;            
    }
}

![85- Maximal Rectangle](images/85- Maximal%20Rectangle.png)

