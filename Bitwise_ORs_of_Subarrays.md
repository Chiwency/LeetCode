## [子数组按位或操作](https://leetcode-cn.com/problems/bitwise-ors-of-subarrays/)

暴力不接受O(n2)的算法，暴力搜索会导致超时



### 代码实现

```go
func subarrayBitwiseORs(arr []int) int {
	visit := make(map[int]bool)
	l := len(arr)
	dp := make([]int, l)
	for i := 0; i < l; i++ {
		visit[arr[i]] = true
		dp[i] = arr[i]
		for j := i - 1; j >= 0; j-- {
			if dp[j] == (dp[j] | arr[i]) {
				break
			}
			dp[j] |= arr[i]
			visit[dp[j]] = true
		}
	}
	return len(visit)
}
```

