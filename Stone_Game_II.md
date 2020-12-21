## [石子游戏 II](https://leetcode-cn.com/problems/stone-game-ii/)

定义dp数组，找出状态转移方程有亿点点难，琢磨题解先

用`dp[i][M]` 表示`piles[i:]` 某人取能获得石头数的最大值（**一般博弈问题，可以不用分两人的情况定义两个`dp数组`，可以用数学方法化解**），那时一次性可取的堆数是M

则状态转移方程为：

```go
if i+2M > len(piles) {
    dp[i][M] = sum[i:]
} else {
    dp[i][M] = max(dp[i][M], sum[i:] - dp[i+x][max(x,M))
}
```



### 代码实现

```go
func stoneGameII(piles []int) int {
	l := len(piles)
	dp := make([][]int, l)
	for k := range dp {
		dp[k] = make([]int, l+1)    // 注意一些边界问题
	}
	sum := 0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := l - 1; i >= 0; i-- {
		sum += piles[i]
		for M := 1; M <= l; M++ {
			if i+2*M >= l {
				dp[i][M] = sum
			} else {
				for x := 1; x <= 2*M; x++ {
					dp[i][M] = max(dp[i][M], sum-dp[i+x][max(x, M)])
				}
			}
		}
	}
	return dp[0][1]
}
```

