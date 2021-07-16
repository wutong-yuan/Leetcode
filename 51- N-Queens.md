# 51. N-Queens

**# 51. N-Queens**# 

**_Consider the columns only because we assume the first queue in the first row, second queue in the second row…._**
**_Then this problem becomes a permutation of the columns _**

class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        List<Integer> colPositionList = new ArrayList<>();
        
        placeQueue(n, result, colPositionList);
        return result;
    }
    
    private void placeQueue(int n, List<List<String>> result, List<Integer> colPositionList) {
        if (colPositionList.size() == n) {
            List<String> solution = getSolution(colPositionList);
            result.add(new ArrayList<>(solution));
        }
        
        for (int colIndex = 0; colIndex < n; colIndex++) {
            if (!isPositionValid(colPositionList, colIndex)) {
                continue;
            }
            
            colPositionList.add(colIndex);
            placeQueue(n, result, colPositionList);
            colPositionList.remove(colPositionList.size() - 1);
        }
    }
    
    private List<String> getSolution(List<Integer> colPositionList) {
        List<String> solution = new ArrayList<>();
        // convert the column position list to the solution we need in the format that is required
        int row = colPositionList.size();
        int column = row;
        for (int rowIndex = 0; rowIndex < row; rowIndex++) {
            StringBuilder rowList = new StringBuilder();
            // for each row, we see if there is a val at the column. val --> Q, else --> . 
            for (int colIndex = 0; colIndex < colPositionList.size(); colIndex++) {
                int position = colPositionList.get(rowIndex);
                if (colIndex == position) {
                    rowList.append('Q');
                } else {
                    rowList.append('.');
                }
            }
            solution.add(rowList.toString());
        }
        
        return solution;
    }
    
    private boolean isPositionValid(List<Integer> colPositionList, int nextCol) {
        int size = colPositionList.size();
        int nextRow = size;
        
        if (colPositionList.contains(nextCol)) {
            return false;
        }
        for (int usedRow = 0; usedRow < size; usedRow++) {
            int usedCol = colPositionList.get(usedRow);
            if ((usedCol + usedRow) == (nextRow + nextCol)) {
                return false;
            }
            
            if ((usedCol - usedRow) == (nextCol - nextRow)) {
                return false;
            }
        }
        
        return true;
    }
}
