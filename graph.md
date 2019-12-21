[1042. Flower Planting With No Adjacent](https://leetcode.com/problems/flower-planting-with-no-adjacent/)
```ruby
def garden_no_adj(n, paths)
    map = {}
    for i in 0...n
        map[i] = Set.new()
    end
    
    paths.each do |path|
        x = path[0] - 1
        y = path[1] - 1
        map[x] << y
        map[y] << x
    end
    
    res = Array.new(n, 0)
    
    for i in 0...n
        colors = Array.new(5)
        map[i].each do |neighbor|
            colors[res[neighbor]] = 1
        end
        
        c = 4
        while c >= 1
            res[i] = c if colors[c] != 1
            c -= 1
        end
    end
    res
end
```

[997. Find the Town Judge](https://leetcode.com/problems/find-the-town-judge/)
```ruby
def find_judge(n, trust)
    count = Array.new(n + 1, 0)
    
    trust.each do |t|
        count[t[0]] -= 1
        count[t[1]] += 1
    end
    
    for i in 1...count.length 
        return i if count[i] == n - 1
    end
    -1
end
```