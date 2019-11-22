[223. Rectangle Area](https://leetcode.com/problems/rectangle-area/)
```ruby
def compute_area(a, b, c, d, e, f, g, h)
    areaA = (c-a) * (d-b)
    areaB = (g-e) * (h-f)
    
    left = [a, e].max
    right = [c, g].min
    bottom = [b, f].max
    top = [d, h].min
    
    overlap = 0
    overlap = (right-left) * (top-bottom) if right > left && top > bottom

    areaA + areaB - overlap
end
```