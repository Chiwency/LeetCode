## [插入区间](https://leetcode-cn.com/problems/insert-interval/)

 用了切片排序简化了下思路，也挺简单的



### 代码实现

```go
func insert(intervals [][]int, newInterval []int) (ans [][]int) {
	intervals = append(intervals, newInterval)
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][0] < intervals[j][0]
	})
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	left := intervals[0][0]
	right := intervals[0][1]
	l := len(intervals)
	for i := 1; i < l; i++ {
		right = max(right, intervals[i-1][1])
		if intervals[i][0] > right {
			ans = append(ans, []int{left, right})
			left = intervals[i][0]
		}
		if i == l-1 {
			right = max(right, intervals[i][1])
			ans = append(ans, []int{left, right})
		}
	}
	if len(intervals) == 1 {
		ans = append(ans, []int{left, right})
	}
	return ans
}
```

