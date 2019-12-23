[1119. Remove Vowels from a String](https://leetcode.com/problems/remove-vowels-from-a-string/)
```ruby
def remove_vowels(s)
    ans = ""
    vowels = "aeiou"
    s.each_char{ |c| ans += c if !vowels.include?(c) }
    ans
end
```

[1108. Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/)

```ruby
def defang_i_paddr(address)
    address.split(".").join("[.]")
end
```