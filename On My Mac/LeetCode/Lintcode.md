# Lintcode
**38 · Search a 2D Matrix II**
**
**
**Description**
Write an efficient algorithm that searches for a value in an m x n matrix, return The number of occurrence of it.
This matrix has the following properties:
* Integers in each row are sorted from left to right.
* Integers in each column are sorted from up to bottom.
* No duplicate integers in each row or column.

**Example**
**Example 1:**

Input:
matrix = [[3,4]]
target = 3
Output:
1
Explanation:
There is only one 3 in the matrix.
**Example 2:**

Input:
matrix = [
      [1, 3, 5, 7],
      [2, 4, 7, 8],
      [3, 5, 9, 10]
    ]
target = 3
Output:
2
Explanation:
There are two 3 in the matrix.
**Challenge**
O(m+n) time and O(1) extra space

https://www.jiuzhang.com/problem/search-a-2d-matrix-ii/ 
**## 算法：搜索/模拟**
根据题意，每行中的整数从左到右是排序的，每一列的整数从上到下是排序的，在每一行或每一列中没有重复的整数。那么我们只要从矩阵的左下角开始向右上角找，若是小于target就往右找，若是大于target就往上找
* 从左下角即(n-1,0)处出发
* 如果matrix[x][y] < target 下一步往右搜
* 如果matrix[x][y] > target 下一步往上搜
* 如果matrix[x][y] = target 下一步往[x-1][y+1]即右上角搜，因为是有序的，每一行每一列中每个数都是唯一的

**## 复杂度分析**
* 时间复杂度O(n+m)
	* 左下角往右上角呈阶梯状走，长度为n+m
* 空间复杂度O(size(matrix))
	* 地图的大小

**public** **class** **Solution** {
    /**
     * **@param** matrix: A list of lists of integers
     * **@param** target: An integer you want to search in matrix
     * **@return**: An integer indicate the total occurrence of target in the given matrix
     */
    **public** **int** **searchMatrix**(**int**[][] matrix, **int** target) {
        **int** ans = 0;
        **int** n = matrix.length,m = matrix[0].length;
        **if** (n == 0 || m==0) {
            **return** 0;
        }
        //从左下角往右上角走，(x,y)=(n-1,0)
        **int** x = n - 1,y = 0;
        **while** (x >= 0 && y < m) {
            //如果matrix[x][y]等于target，则找到一个相等的值，由于严格排序，直接跳到右上角继续搜
            **if** (matrix[x][y] == target) {
                ans++;
                x--;
                y++;
            }
            //如果matrix[x][y]比target大，则往上走
            **else** **if** (matrix[x][y] > target) {
                x--;
            }
            //如果matrix[x][y]比target小，则往右走
            **else** {
                y++;
            }
        }
        **return** ans;
    }
}

