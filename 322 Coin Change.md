# 322. Coin Change

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1

```

**Example 3:**

```
Input: coins = [1], amount = 0
Output: 0

```

**Example 4:**

```
Input: coins = [1], amount = 1
Output: 1

```

**Example 5:**

```
Input: coins = [1], amount = 2
Output: 2

```

**Constraints:**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`

Top down sol:

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if not amount:
            return amount
        coins.sort()
        coinSet = set(coins)
        self.mem = {}
        def help(a):
            if a in self.mem:
                return self.mem[a]
                
            if a < coins[0]:
                return -1
            elif a in coinSet:
                return 1
            res = float('inf')
            for c in coins:
                if a - c >= 0:
                    tmp = help(a - c)
                    if tmp == -1:
                        continue
                    else:
                        res = min(res, help(a - c) + 1)
            if res == float('inf'):
                self.mem[a] = -1
                return -1            
            self.mem[a] = res
            return res
        
        return help(amount)
```

button up sol:

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if not amount:
            return amount
        dp = [-1] * (amount + 1)
        coins.sort()
        coinSet = set(coins)
        for c in range(1, amount + 1):
            if c < coins[0]:
                continue
            elif c in coinSet:
                dp[c] = 1
            else:
                dp[c] = float('inf')
                for coin in coins:
                    if c - coin >= 0 and dp[c - coin] != -1:
                        dp[c] = min(dp[c], dp[c - coin] + 1)
                if dp[c] == float('inf'):
                    dp[c] = -1
        return dp[-1]
```