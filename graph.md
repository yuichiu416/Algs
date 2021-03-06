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
# topology sort approach, slow
def can_finish(num_courses, prerequisites)
    matrix = Array.new(num_courses) { Array.new(num_courses, 0)}
    indegree = Array.new(num_courses, 0)
    
    for i in 0...prerequisites.length
        ready = prerequisites[i][0]
        pre = prerequisites[i][1]
        indegree[ready] += 1 if matrix[pre][ready] == 0
        matrix[pre][ready] = 1
    end
       
    count = 0
    queue = []
    for i in 0...indegree.length
        queue << i if indegree[i] == 0
    end
    
    while !queue.empty?
        course = queue.shift
        count += 1
        for i in 0...num_courses
            if matrix[course][i] != 0
                indegree[i] -= 1
                queue << i if indegree[i] == 0
            end
        end
    end
    count == num_courses
end
```

```ruby
# dfs approach, slow too
def can_finish(num_courses, prerequisites)
    graph = Array.new(num_courses){ Array.new(0)}
    for i in 0...prerequisites.length
        graph[prerequisites[i][1]] << prerequisites[i][0]
    end
    visited = Array.new(num_courses, false)
    for i in 0...num_courses
        return false if !dfs(graph, visited, i)
    end
    true
end

def dfs(graph, visited, course)
    if visited[course]
        return false
    else
        visited[course] = true
    end
    for i in 0...graph[course].length
        return false if !dfs(graph, visited, graph[course][i])
    end
    visited[course] = false
    true
end
```

```ruby
# fast dfs using hash
def can_finish(num_courses, prerequisites)
    map = {}
    prerequisites.each do |prereq|
        map[prereq[0]] ||= []
        map[prereq[0]] << prereq[1]
    end
    visited = []
    visiting = []
    map.each do |course, prereqs|
        if dfs(visited, visiting, course, prereqs, map)
            return false
        end
    end
    true
end

def dfs(visited, visiting, course, prereqs, map)
    visited[course] = visiting[course] = true
    prereqs.each do |prereq|
        if visited[prereq] && visiting[prereq]
            return true
        elsif !visited[prereq] && dfs(visited, visiting, prereq, map[prereq] || [], map)
            return true
        end
    end
    visiting[course] = false
    false
end
```

[210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
```ruby
def find_order(n, prereqs)
    @graph = Hash.new { |h, k| h[k] = Set.new() }
    @visited, @on_stack, @result = Set.new(), Set.new(), []
    prereqs.each { |u, v| @graph[u].add(v) }
    n.times { |node| return [] if !@visited.include?(node) && dfs_has_cycle?(node) } # find one not visited and start from it
    @result.size == n ? @result : []
end

def dfs_has_cycle?(node)
    @visited.add(node)
    @on_stack.add(node)
    @graph[node].each do |v|
        return true if @on_stack.include?(v)
        return true if !@visited.include?(v) && dfs_has_cycle?(v)
    end
    @result.push(node)
    @on_stack.delete(node) # Making DFS a post-order traversal: popping current when all its children are done
    false
end
```

[802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/)
```ruby
def eventual_safe_nodes(graph)
    res = []
    visited = Array.new(graph.size)
    (0...graph.size).each do |i|
       res << i if !cycle(i, graph, visited) 
    end
    res
end

def cycle(node, graph, visited)
    return false if visited[node] == 1
   return true if visited[node] == -1
    
    visited[node] = -1
    
    graph[node].each do |neigh|
       return true if cycle(neigh, graph, visited)
    end
    
    visited[node] = 1
    
    return false
end
```