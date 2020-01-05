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

[13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
```ruby
def roman_to_int(s)
    nums = Array.new(s.length)
    for i in 0...s.length
        case s[i]
            when "M"
                nums[i] = 1000
            when "D"
                nums[i] = 500
            when "C"
                nums[i] = 100
            when "L"
                nums[i] = 50
            when "X"
                nums[i] = 10
            when "V"
                nums[i] = 5
            when "I"
                nums[i] = 1
        end
    end
    sum = 0
    for i in 0...nums.length - 1
        if nums[i] < nums[i + 1]
            sum -= nums[i]
        else
            sum += nums[i]
        end
    end
    sum + nums[-1]
end
```

[819. Most Common Word](https://leetcode.com/problems/most-common-word/)
```java
class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        Map<String, Integer> map = new HashMap();
        
        String[] words = paragraph.replaceAll("\\W+", " ").toLowerCase().split("\\s+");
        Set ban = new HashSet<>(Arrays.asList(banned));
        
        for(String word : words){
            if(!ban.contains(word)){
                    map.put(word, map.getOrDefault(word, 0) + 1);
            }
        }
        
        return Collections.max(map.entrySet(), Map.Entry.comparingByValue()).getKey();
    }
}
```