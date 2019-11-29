[322. Coin Change](https://leetcode.com/problems/coin-change/)

```ruby
def coin_change(coins, amount)
    return -1 if coins.nil? || coins.empty? || amount < 0
    dp = Array.new(amount + 1, -1)
    dp[0] = 0
    
    coins.each do |coin|
        for amt in coin..amount
            next if dp[amt - coin] == -1
            dp[amt] = dp[amt - coin] + 1 if dp[amt] == -1 || dp[amt - coin] + 1 < dp[amt]
        end
        
    end
    dp[-1]
end
```

[139. Word Break](https://leetcode.com/problems/word-break/)
```ruby
def word_break(s, word_dict)
    return false if s.nil? || s.length == 0
    dp = Array.new(s.length, false)
    for right in 0...s.length
        for left in 0..right
            if word_dict.include?(s[left..right]) && (left == 0 || dp[left - 1])
                dp[right] = true
                break
            end
        end
    end
    dp[-1]
end
```