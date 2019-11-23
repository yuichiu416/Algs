[289. Game of Life](https://leetcode.com/problems/game-of-life/)

```java
class Solution {
    public void gameOfLife(int[][] board) {
        if(board == null || board[0] == null){
            return;
        }
        int height = board.length, width = board[0].length;
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                helper(board, i, j, height, width);

            }
        }
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                board[i][j] %= 2;
            }
        }
    }
    
    private void helper(int[][] board, int row, int col, int height, int width){
        int lives = 0, dead = 0;
        for(int i = -1; i < 2; i++){
            for(int j = -1; j < 2; j++){
                if(i == 0 && j == 0){
                    continue;
                }
                if(row + i < 0 || row + i >= height){
                    continue;
                } else if(col + j < 0 || col + j >= width){
                    continue;
                }
                if(board[row + i][col + j] == 1 || board[row + i][col + j] == 2){
                    lives++;
                } else{
                    dead++;
                }
            }
        }
        // 0: dead
        // 1: live
        // 2: live, go dead
        // 3: dead, go live
        if(board[row][col] == 1){
            if(lives < 2 || lives > 3){
                board[row][col] = 2;
            }
        } else{
            if(lives == 3){
                board[row][col] = 3;

            }
        }
    }
}
```

[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] ans = new int[nums.length];
        ans[0] = 1;
        for(int i = 1; i < nums.length; i++){
            ans[i] = ans[i - 1] * nums[i - 1];
        }
        int right = 1;
        for(int i = nums.length - 2; i >= 0; i--){
            right *= nums[i + 1];
            ans[i] *= right;
        }
        return ans;
    }
}
```