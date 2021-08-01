# class Solution {

# 

class Solution {
    int used = 1;
    int unUsed = 0;
    int size = 0;
    
    public int totalNQueens(int n) {
        
        if (n == 1) return 1;
        size = n;
        
        Set<Integer> usedCol = new HashSet<>();
        Set<Integer> usedDiagonals = new HashSet<>();
        Set<Integer> usedAntiDiagonals = new HashSet<>();
        
        int result = placeQueue(0, usedCol, usedDiagonals, usedAntiDiagonals);        
        return result;       
    }
    
    private int placeQueue(int row, Set<Integer> usedCol, Set<Integer> usedDiagonals, Set<Integer> usedAntiDiagonals) {
        if (row == size) {
            return 1;
        }
        
        int solution = 0;
        
        for (int col = 0; col < size; col++) {
            int currDiagnoal = row - col;
            int antiDiagnoal = row + col;
            
            if (usedCol.contains(col) ||
               usedDiagonals.contains(currDiagnoal) ||
               usedAntiDiagonals.contains(antiDiagnoal)) {
                continue;
            }
            
            usedCol.add(col);
            usedDiagonals.add(currDiagnoal);
            usedAntiDiagonals.add(antiDiagnoal);
            solution += placeQueue(row + 1, usedCol, usedDiagonals, usedAntiDiagonals);
            usedCol.remove(col);
            usedDiagonals.remove(currDiagnoal);
            usedAntiDiagonals.remove(antiDiagnoal);
        }
        
        return solution;
    }
    
}
