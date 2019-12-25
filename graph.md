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

[1267. Count Servers that Communicate](https://leetcode.com/problems/count-servers-that-communicate/)
```ruby
def count_servers(grid)
    return 0 if grid.nil? || grid.length == 0 || grid[0].length == 0
    rowLen = grid.length
    colLen = grid[0].length
    rows = Array.new(rowLen, 0)
    cols = Array.new(colLen, 0)
    servers = 0
    for i in 0...rowLen
        for j in 0...colLen
            if grid[i][j] == 1
                rows[i] += 1
                cols[j] += 1
                servers += 1
            end
        end
    end
    
    for i in 0...rowLen
        for j in 0...colLen
            servers -= 1 if grid[i][j] == 1 && rows[i] == 1 && cols[j] == 1
        end
    end
    servers
end
```

[207. Course Schedule](https://leetcode.com/problems/course-schedule/)
```ruby
# dfs approach
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
    true
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
    false
end

# bfs approach
def can_finish(num_courses, prerequisites)
    matrix  = Array.new(num_courses) {[]}
    indegree = [0] * num_courses
    prerequisites.each do |course, prerequisite|
        matrix[prerequisite][course] = 1
        # number of prerequisite or edges directed to course
        indegree[course] += 1
    end
    
    no_dependency_courses = []
    indegree.each_index {|index| no_dependency_courses << index if indegree[index].zero? }
    
    courses_that_can_be_finish = 0
    while(course = no_dependency_courses.shift)
        courses_that_can_be_finish +=1
        
        matrix[course].each.with_index do |has_edge, dependent_course|
            if has_edge == 1
                indegree[dependent_course] -= 1
                no_dependency_courses << dependent_course if indegree[dependent_course].zero?
            end
        end
    end

    courses_that_can_be_finish == num_courses
end
```