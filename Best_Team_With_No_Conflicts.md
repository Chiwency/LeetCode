## [无矛盾的最佳球队](https://leetcode-cn.com/problems/best-team-with-no-conflicts/)

用`sort.Slice`实现切片排序，可以通过定义`Less()`函数实现自定义的排序规则

一开始想用map来储存对应关系，再对第一个数组进行排序，但是很难解决重复元素的问题，看了一个题解才发现**先构成二维数组，再排序的方法**



### 代码实现

```go
func bestTeamScore(scores []int, ages []int) int {
	l := len(scores)
	array := make([][2]int, l)
	for k := range array {
		array[k] = [2]int{scores[k], ages[k]}
	}
	sort.Slice(array, func(i, j int) bool {
		return array[i][1] < array[j][1] || (array[i][1] == array[j][1] && array[i][0] < array[j][0])
	})
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	dp := make([]int, l)
	ans := 0
	for k := range array {
		dp[k] = array[k][0]
		for i := 0; i < k; i++ {
			if array[k][0] >= array[i][0] {
				dp[k] = max(dp[k], dp[i]+array[k][0])
			}
		}
		ans = max(ans, dp[k])
	}

	return ans
}
```

