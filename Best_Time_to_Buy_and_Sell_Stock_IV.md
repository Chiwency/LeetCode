## [买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

比较难的动态规划最好先别写优化空间的类型，要先做出，再想优化！！！一步登天的想累死人。

### 代码实现

```go
func maxProfit(k int, prices []int) int {
	l := len(prices)
	if k > l/2 {
		k = l / 2
	}
	if k == 0 {
		return 0
	}
	nohold := make([]int, k+1)
	hold := make([]int, k+1)
	hold[0] = -prices[0]
	max := func(a ...int) int {
		max := a[0]
		for _, v := range a[1:] {
			if v > max {
				max = v
			}
		}
		return max
	}
	for i := 1; i <= k; i++ {
		hold[i] = math.MinInt64 / 2
		nohold[i] = math.MinInt64 / 2
	}

	for i := 1; i < l; i++ {
		hold[0] = max(hold[0], -prices[i])
		for j := 1; j <= k; j++ {
			hold[j] = max(hold[j], nohold[j]-prices[i])     // 头一天持有的或者今天买入的
            // 比如j=5但是最开始nohold[1][5]前面定义了是最小负值
            // 这个nohold[2][5]就有可能是负值了
            // 所以这种算法不一定是交易次数越多的利润越大
            // 下面这种迭代表明，j等于多少就一定要交易多少次，在交易次数固定的时候选择利润最大的
            // 但是prices降序[4,3,2,1]排列的话，nohold[j]就是负值了
			nohold[j] = max(hold[j-1]+prices[i], nohold[j]) // 今天交易或者或者不交易
		}
	}

	return max(nohold...)
}
```

