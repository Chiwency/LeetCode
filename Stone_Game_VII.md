## [石子游戏 VII](https://leetcode-cn.com/problems/stone-game-vii/)

之前总结过，博弈问题都是不要分两种情况讨论的，以各自视角看都要最优。因此设`dp[i][j]`为`stones[i]—stones[j]` 时两者的差值，不管以谁的视角来看，都希望这个差值（不是绝对值）最大。 会赢的那个人希望差值最大，这时候差值一定是正的。输的那个人希望差值最小，这时候差值是负的，也要让负的差值更小。

因此可以得出状态转移方程:

```go
dp[i][j] = max(rightSum-dp[i+1][j], leftSum-dp[i][j-1])
```



### 代码实现

```go
func stoneGameVII(stones []int) int {
	l := len(stones)
	dp := make([][]int, l)
	sum := make([]int, l+1)
	sum[l-1] = stones[l-1]
	for k := range dp {
		dp[k] = make([]int, l)
	}
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}

	for i := l - 2; i >= 0; i-- {
		sum[i] = sum[i+1] + stones[i]
		for j := i + 1; j < l; j++ {
			rightSum := sum[i+1] - sum[j+1]
			leftSum := sum[i] - sum[j]
          // 因为是从右往左遍历，这里dp[i+1][j]可以看成是上一次左指针是i+1，右指针是j对应的dp值,dp[j]
          // dp[i][j-1] 可以看成是本次左指针都是i时，上一个dp值，dp[j-1]
          // 这就是所谓的本层状态只与上层和本层有关，无后效性，可以优化空间
			dp[i][j] = max(rightSum-dp[i+1][j], leftSum-dp[i][j-1])   
		}
	}
	return dp[0][l-1]
}
```



**只需要简单的改动几行代码，就能极大的优化空间**

### 空间优化

```go
func stoneGameVII(stones []int) int {
	l := len(stones)
	dp := make([]int, l)
	sum := make([]int, l+1)
	sum[l-1] = stones[l-1]

	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}

	for i := l - 2; i >= 0; i-- {
		sum[i] = sum[i+1] + stones[i]
		for j := i + 1; j < l; j++ {
			rightSum := sum[i+1] - sum[j+1]
			leftSum := sum[i] - sum[j]
			dp[j] = max(rightSum-dp[j], leftSum-dp[j-1])
		}
	}
	return dp[l-1]
}
```

