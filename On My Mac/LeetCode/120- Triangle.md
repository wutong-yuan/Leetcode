# 120. Triangle

**# https://www.youtube.com/watch?v=OM1MTokvxs4****#  **

**_DC with Memoization_**

class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        Map<String, Integer> seen = new HashMap<>();
        return divideAndConquer(triangle, 0, 0, seen);
    }
    
    private int divideAndConquer(List<List<Integer>> triangle, int row, int col, Map<String, Integer> seen) {
        if (row >= triangle.size()) return 0;
        
        if (seen.containsKey(row + ":" + col)){
            return seen.get(row + ":" + col);
        }
        
        int result = triangle.get(row).get(col) + Math.min(divideAndConquer(triangle, row + 1, col, seen), 
                              divideAndConquer(triangle, row + 1, col + 1, seen));
        seen.put(row + ":" + col, result);
        
        return result;
    }
}

**_In place - top down_**

class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        for (int row = 1; row < n; row++) {
            for (int col = 0; col <= row; col++) {
                int smallestAbove = Integer.MAX_VALUE;
                if (col == 0) {
                    smallestAbove = triangle.get(row - 1).get(col);
                } else if(col == row) {
                    smallestAbove = triangle.get(row - 1).get(col - 1);
                } else {
                    smallestAbove = Math.min(triangle.get(row - 1).get(col - 1), triangle.get(row - 1).get(col));
                }
                
                int path = smallestAbove + triangle.get(row).get(col);
                triangle.get(row).set(col, path);
            }
        }
        return Collections.min(triangle.get(triangle.size() - 1));
    }
}

**_Use Extra space: - top down_**

class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        List<Integer> prevRow = triangle.get(0);
        int m = triangle.size();
        for (int row = 1; row < m; row++) {
            ArrayList<Integer> currentRow = new ArrayList<>();
            for (int col = 0; col <= row; col++) {
                int min = Integer.MAX_VALUE;
                if (col == 0) {
                    min = prevRow.get(col);
                } else if (col == row) {
                    min = prevRow.get(col - 1);
                } else {
                    min = Math.min(prevRow.get(col - 1),
                                  prevRow.get(col));
                }
                
                int currNum = triangle.get(row).get(col);
                
                currentRow.add(col, min + currNum);
            }
            prevRow = currentRow;
        }
        return Collections.min(prevRow);
    }
}

**_In Place - bottom up_**

class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int rows = triangle.size();
        
        for (int row = rows - 2; row >= 0; row--) {
            for (int col = 0; col <= row; col++) {
                int min = Math.min(triangle.get(row + 1).get(col + 1),
                                  triangle.get(row + 1).get(col));
                int currNum = triangle.get(row).get(col);
                triangle.get(row).set(col, min + currNum);
            }
        }
        
        return triangle.get(0).get(0);
    }
}
**_In Place - extra space_**
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        ArrayList<Integer> nextRow = new ArrayList<>();
        int rows = triangle.size();
        List<Integer> lastRow = triangle.get(rows - 1);
        
        for (int i = 0; i < lastRow.size(); i++) {
            nextRow.add(lastRow.get(i));
        }
        
        for (int row = rows - 2; row >= 0; row--) {
            ArrayList<Integer> currRow = new ArrayList<>();
            for (int col = 0; col <= row; col++) {
                int currNum = triangle.get(row).get(col);
                int min = Math.min(nextRow.get(col), nextRow.get(col + 1));
                currRow.add(col, currNum + min);
            }
            nextRow = currRow;
        }
        return nextRow.get(0);
    }
}

