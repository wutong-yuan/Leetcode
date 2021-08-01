# 240 Search a 2D Matrix II

# 240 **# Search a 2D Matrix II**# 

**_Use Jiuzhang approach:_**

class Solution {

    public boolean searchMatrix(int[][] matrix, int target) {
        
        int rows = matrix.length;
        int columns = matrix[0].length;
        int x = rows - 1;
        int y = 0;
        
        while (x >= 0 && y < columns) {
            if(matrix[x][y] == target) {
                return true;
            }
            if(matrix[x][y] < target) {
                y++;
            } else{
                x--;
            }
        }
        return false;
    }
}
