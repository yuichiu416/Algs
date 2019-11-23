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