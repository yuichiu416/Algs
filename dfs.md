[289. Game of Life](https://leetcode.com/problems/game-of-life/)
```java
class Solution {
    public void gameOfLife(int[][] board) {
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                check(board, i, j);
            }
        }
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                board[i][j] %= 2;
            }
        }
    }
    
    private void check(int[][] board, int row, int col){
        int count = 0;
        for(int i = -1; i < 2; i++){
            for(int j = -1; j < 2; j++){
                if(i == 0 && j == 0)
                    continue;
                if(inBound(board, row + i, col + j, board.length, board[0].length)){
                    if(board[row + i][col + j] == 1 || board[row + i][col + j] == 2)
                        count++;
                }
            }
        }
        if(board[row][col] == 0){
            if(count == 3){
                board[row][col] = 3;
            }
        } else{
            if(count < 2 || count > 3){
                board[row][col] = 2;
            }
        }
        
    }
    private boolean inBound(int[][] board, int i, int j, int iMax, int jMax){
        if(i >= 0 && i < iMax && j >= 0 && j < jMax)
            return true;
        else
            return false;
    }
}
```