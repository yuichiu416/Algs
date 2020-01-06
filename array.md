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

[12. Integer to Roman](https://leetcode.com/problems/integer-to-roman/)

```java
class Solution {
    public static String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
    }
}
```

[1013. Partition Array Into Three Parts With Equal Sum](https://leetcode.com/problems/partition-array-into-three-parts-with-equal-sum/)

```ruby
def can_three_parts_equal_sum(a)
    return if a.empty? || a.length <= 3
    sum = a.sum
    return false if sum % 3 != 0
    scanner = 0
    ctr = 0
    a.each do |n|
        scanner += n
        if scanner == sum / 3
            ctr += 1
            scanner = 0
        end
    end
    ctr == 3
end
```

```ruby
def remove_duplicates(nums)
    return 0 if nums.nil? || nums.length < 1
    left, right = 1, 1
    while right < nums.length
       if(nums[right] != nums[right - 1])
           nums[left] = nums[right]
           left += 1
       end
        right += 1
    end
    left
end
```

[922. Sort Array By Parity II](https://leetcode.com/problems/sort-array-by-parity-ii/)
```ruby
def sort_array_by_parity_ii(a)
    return a if a.nil? || a.length == 0
    odd, even, idx = 1, 0, a.length
    while odd < idx && even < idx
        while odd < idx && a[odd].odd?
            odd += 2
        end
        while even < idx && a[even].even?
            even += 2
        end
        a[odd], a[even] = a[even], a[odd] if odd < idx && even < idx
    end
    a
end
```

[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
```ruby
def fib(n)
    arr = [0, 1]
    while arr.length < n + 1
        arr << arr[-1] + arr[-2]
    end
    arr[n]
end
```

[841. Keys and Rooms](https://leetcode.com/problems/keys-and-rooms/)
```ruby
def can_visit_all_rooms(rooms)
    stack = [0]
    seen = Set.new()
    seen << 0
    while !stack.empty?
        room = stack.pop
        rooms[room].each do |i|
            if !seen.include?(i)
                stack << i
                seen << i
                return true if rooms.length == seen.length
            end
        end
    end
    rooms.length == seen.length
end
```

[1. Two Sum](https://leetcode.com/problems/two-sum/)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap();
        int[] ans = new int[2];
        
        for(int i = 0; i < nums.length; i++){
            Integer temp = map.get(nums[i]);
            if(temp != null){
                return new int[]{temp, i};
            } else{
                map.put(target - nums[i], i);
            }
        }
        return null;
    }
}
```
[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
```java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int left = 0, right = points.length - 1;
        
        while(left <= right){
            int idx = helper(points, left, right);
            if(idx < K){
                left = idx + 1;
            } else if (idx > K){
                right = idx - 1;
            } else{
                break;
            }
        }
        return Arrays.copyOfRange(points, 0, K);
    }
    
    private int helper(int[][] points, int left, int right){
        int[] pivot = points[left];
        while(left < right){
            while(left < right && distance(points[right], pivot) >= 0)
                right--;
            points[left] = points[right];
            while( left < right && distance(points[left], pivot) <= 0)
                left++;
            points[right] = points[left];
        }
        points[left] = pivot;
        return left;
    }
    
    private int distance(int[] p1, int[]p2){
        return p1[0] * p1[0] + p1[1] * p1[1] - p2[0] * p2[0] - p2[1] * p2[1];
    }
}
```
[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length - 1, max = 0;
        while(left < right){
            int volume = (right-left) * Math.min(height[left], height[right]);
            if(volume > max)
                max = volume;
            if(height[left] < height[right])
                left++;
            else
                right--;
        }
        return max;
    }
}
```