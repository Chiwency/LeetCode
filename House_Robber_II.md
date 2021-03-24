## [打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

很明显的动规，问题就在于对最后一家的判断，如何确定之前的状态中是否有打劫过第一家，我直接维护了两个dp数组，第二个dp数组就不包含第一家，用于判断最后一家是否可以打劫   但是太费空间了，，，，，有点蠢的方法

看到精选题解是循环遍历两次 一样的思路 他是时间换空间

但是发现这道题可以用滚动数组思想把时间复杂度降到常数级

那用我这种空间换时间的方法，就只需要四个变量就可，O(1)的空间复杂度，循环遍历一次 完美！



### 代码实现

```go
func rob(nums []int) int {
	l := len(nums)
	dp := make([][2]int, l)
	dp[0][0] = nums[0]
	dp[0][1] = 0
	for i := 1; i < l; i++ {
		if i < 2 {
			dp[i][0] = max(dp[i-1][0], nums[i])
			dp[i][1] = max(dp[i-1][1], nums[i])
		} else if i == l-1 {
			dp[i][0] = max(dp[i-2][1]+nums[i], dp[i-1][0])
		} else {
			dp[i][0] = max(dp[i-2][0]+nums[i], dp[i-1][0])
			dp[i][1] = max(dp[i-2][1]+nums[i], dp[i-1][1])
		}
	}
	return dp[l-1][0]
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

