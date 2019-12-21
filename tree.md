[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
```ruby
def min_depth(root)
    return 0 if root.nil?
    left = min_depth(root.left)
    right = min_depth(root.right)
    (left == 0 || right == 0) ? left + right + 1 : [left, right].min + 1
end
```

[1161. Maximum Level Sum of a Binary Tree](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/)
```ruby
def max_level_sum(root, hash = Hash.new(0), level = 1, max = [0])
    return 1 if root.nil?
    hash[level] += root.val
    max_level_sum(root.left, hash, level + 1, max)
    max_level_sum(root.right, hash, level + 1, max)
    maxLevel, max = 0, 0
    if level == 1
        hash.each do |k, v|
            if v > max
                max = v
                maxLevel = k
            end
        end
    end
    maxLevel
end
```