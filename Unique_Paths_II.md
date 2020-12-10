## [不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

设``dp[i][j]`` 为``obstacleGrid[i][j]``到终点的不同路径数

状态转移方程为：

```go
dp[i][j]=dp[i+1][j]+dp[i][j+1]
```



### 代码实现

```go
func uniquePathsWithObstacles(obstacleGrid [][]int) int {
	m := len(obstacleGrid)
	n := len(obstacleGrid[0])
	dp := make([][]int, m+1)
	for i := 0; i < m+1; i++ {
		dp[i] = make([]int, n+1)
	}
	// 让后面dp[m-1][n-1]=1
	dp[m][n-1] = 1
	for i := m - 1; i >= 0; i-- {
		for j := n - 1; j >= 0; j-- {
			// 如果在障碍点，则路径为0
			if obstacleGrid[i][j] == 1 {
				dp[i][j] = 0
			} else {
				dp[i][j] = dp[i+1][j] + dp[i][j+1]
			}
		}
	}
	return dp[0][0]
}
```

**这样写比较简单，也可以用滚动数组思想把空间复杂度再降一级，但是最开始只想到这种，就先记录这种**