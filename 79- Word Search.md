# 79. Word Search

**79. Word Search **

https://www.youtube.com/watch?v=pfiQ_PS1g8E&t=476s 

See paper notes to understand the unmark line

        visited[i][j] = true;
        boolean result = (backtrack(board, word, i + 1, j, index + 1, visited) ||
                          backtrack(board, word, i - 1, j, index + 1, visited) ||
                          backtrack(board, word, i, j + 1, index + 1, visited) ||
                          backtrack(board, word, i, j - 1, index + 1, visited));
   **     visited[i][j] = false;**

**_With extra space for visited:_**

class Solution {
    public boolean exist(char[][] board, String word) {
        int r = board.length;
        int c = board[0].length;
        boolean[][] visited = new boolean[r][c];
        
        for (int i = 0; i < r; i++) {
            for(int j = 0; j < c; j++) {
                if(backtrack(board, word,i,j,0, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    public boolean backtrack(char[][] board, String word, int i, int j, int index, boolean[][] visited) {
        
        if(index == word.length()) return true;
        int r = board.length;
        int c = board[0].length;
        if(i >= r || j >= c ) return false;
        if(i < 0 || j < 0) return false;
        if(visited[i][j]) return false;
        if(board[i][j] != word.charAt(index)) return false;
        
        visited[i][j] = true;
        boolean result = (backtrack(board, word, i + 1, j, index + 1, visited) ||
                          backtrack(board, word, i - 1, j, index + 1, visited) ||
                          backtrack(board, word, i, j + 1, index + 1, visited) ||
                          backtrack(board, word, i, j - 1, index + 1, visited));
        visited[i][j] = false;
        
        return result;
    }
}

**_Without extra space for visited:_**
public boolean exist(char[][] board, String word) {
    char[] w = word.toCharArray();
    for (int y=0; y<board.length; y++) {
    	for (int x=0; x<board[y].length; x++) {
    		if (exist(board, y, x, w, 0)) return true;
    	}
    }
    return false;
}

private boolean exist(char[][] board, int y, int x, char[] word, int i) {
	if (i == word.length) return true;
	if (y<0 || x<0 || y == board.length || x == board[y].length) return false;
	if (board[y][x] != word[i]) return false;
	board[y][x] ^= 256;
	boolean exist = exist(board, y, x+1, word, i+1)
		|| exist(board, y, x-1, word, i+1)
		|| exist(board, y+1, x, word, i+1)
		|| exist(board, y-1, x, word, i+1);
	board[y][x] ^= 256;
	return exist;
}
## 

## 

