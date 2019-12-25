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
# fast dfs
def can_finish(num_courses, prerequisites)
    map = {}
    prerequisites.each do |course, prerequisite|
        map[course] ||= []
        map[course] << prerequisite
    end

    visited = []
    stepped = []
    map.each do |course, prerequisites|
        return false if dfs(visited, stepped, course, prerequisites, map)
    end
    return true
end

def dfs(visited, stepped, course, prerequisites, map)
    # Mark Course Visited, and implies edges visited
    # Mark coursed as current in step
    visited[course] = stepped[course] = true
    prerequisites.each do |prerequisite|
        if ((visited[prerequisite] && stepped[prerequisite]) || !visited[prerequisite] && dfs(visited, stepped, prerequisite, map[prerequisite]||[], map))
            return true
        end
    end
    stepped[course] = false
    return false
end
```