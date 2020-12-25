## [最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

用`dp[i]`表示`price[i]-price[l-1]`期间买卖股票的最大利润，然后不断向前推进，则可以很自然的想到状态转移方程:

> 一些常见的很明显的动态规划问题都是从后向前推，找对套路就很简单

```go
dp[i]=max(dp[j],prices[j]-prices[i]+dp[j+2],dp[i])   
```



## 代码实现

```go
func maxProfit(prices []int) int {
	l := len(prices)
	dp := make([]int, l+2)
	max := func(a, b, c int) int {
		if a > b && a > c {
			return a
		} else if b > a && b > c {
			return b
		} else {
			return c
		}
	}

	for i := l - 2; i >= 0; i-- {
		for j := i + 1; j < l; j++ {
			dp[i] = max(dp[j], prices[j]-prices[i]+dp[j+2], dp[i])
		}
	}
	return dp[0]
}
```

