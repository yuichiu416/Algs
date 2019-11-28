111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
```ruby
def min_depth(root)
    return 0 if root.nil?
    left = min_depth(root.left)
    right = min_depth(root.right)
    (left == 0 || right == 0) ? left + right + 1 : [left, right].min + 1
end
```