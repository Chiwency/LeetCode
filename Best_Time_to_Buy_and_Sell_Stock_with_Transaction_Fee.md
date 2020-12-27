## [买卖股票的最佳时机含手续费](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

之前有一种很容易想到的算法，从后往前迭代，但是时间复杂度是O(n2),报了超时的错误。

直接看O(n)的算法。用`dp[i][0]`表示此时手中没有股票时的最大利润。`dp[i][1]`表示手中持有股票时的最大利润。下面可以分别得出两个dp数组的状态转移方程:

```go
dp[i][0]=max(dp[i-1][0],dp[i-1][1]+prices[i]-fee)
dp[i][1]=max(dp[i-1][1],dp[i-1][0]-prices[i])  // 前一天买入的或者之前就持有的，看哪个剩余利润更大
```

可以发现状态转移是无后效性的，优化空间

### 代码实现

```go
func maxProfit(prices []int, fee int) int {
	l := len(prices)
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}

	nohold := 0
	hold := -prices[0]
	for i := 1; i < l; i++ {
		nohold = max(nohold, hold+prices[i]-fee)
		hold = max(hold, nohold-prices[i])
	}

	return nohold
}
```

