## [石子游戏](https://leetcode-cn.com/problems/stone-game/)

设 ``dp[i][j]`` 表示从piles[i]—piles[j] 两个玩家的拥有石头的差值. 

因为是石头堆数是偶数，`Alex` 先手所以最后`dp[0][l-1]` 我就可以认定是`Alex-Lee` 的剩余石头数

则状态转移方程为：

```go java
dp[i][j]=max(piles[i]-dp[i-1][j],piles[j]-dp[i][j-1])
```



### 代码实现

```go
func stoneGame(piles []int) bool {
	l := len(piles)
	dp := make([][]int, l)
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := 0; i < l; i++ {
		dp[i] = make([]int, l)
		dp[i][i] = piles[i]
	}
	for i := l - 2; i >= 0; i-- {
		for j := i + 1; j < l; j++ {
			dp[i][j] = max(piles[i]-dp[i+1][j], piles[j]-dp[i][j-1])
		}
	}

	return dp[0][l-1]>0
}
```



## 空间优化

```go
func stoneGame(piles []int) bool {
    l := len(piles)
    dp := make([]int, l)
    max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
    for i := 0; i < length; i++ {
        dp[i] = piles[i]
    }
    for i := length - 2; i >= 0; i-- {
        for j := i + 1; j < length; j++ {
            dp[j] = max(piles[i] - dp[j], piles[j] - dp[j - 1])
        }
    }
    return dp[length - 1] > 0
}
```

