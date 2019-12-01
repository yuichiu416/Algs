[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
```ruby
def add_two_numbers(l1, l2)
    dummy = ListNode.new(0)
    ptr = dummy
    carry = 0
    while !l1.nil? || !l2.nil?
        v1 = l1.nil? ? 0 : l1.val
        v2 = l2.nil? ? 0 : l2.val
        sum = v1 + v2 + carry
        digit = sum % 10
        carry = sum / 10
        
        ptr.next = ListNode.new(digit)
        ptr = ptr.next
        l1 = l1.next if !l1.nil?
        l2 = l2.next if !l2.nil?
    end
    ptr.next = ListNode.new(carry) if carry != 0
    dummy.next
end
```