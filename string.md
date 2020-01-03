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

[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
```ruby
def longest_palindrome(s)
    return s if s.nil? || s.length <= 1
    longest = [""]
    for i in 0...s.length
        check_palindrome(s, i, i, longest)
        check_palindrome(s, i, i + 1, longest)
    end
    longest[0]
end

def check_palindrome(s, left, right, longest)
    while left >= 0 && right < s.length
        if s[left] == s[right]
            left -= 1
            right += 1
        else
            break
        end
    end
    left += 1
    right -= 1
    longest[0] = s[left..right] if right - left + 1 > longest[0].length
end
```