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
# traverse approach
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

```ruby
# BFS approach
def max_level_sum(root)
    queue = [root]
    current_level, max_level, max_sum = 1, 1, root.val
    while !queue.empty?
        level_sum = 0
        queue.length.times do
            node = queue.shift
            level_sum += node.val
            queue << node.left if node.left
            queue << node.right if node.right
        end
        if level_sum > max_sum
            max_sum = level_sum 
            max_level = current_level
        end
        current_level += 1
    end
    max_level
end
```