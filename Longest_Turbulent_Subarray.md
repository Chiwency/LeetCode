## [最长湍流子数组](https://leetcode-cn.com/problems/longest-turbulent-subarray/)

滑动窗口题，用了位运算使代码更简洁了，位运算牛逼！！！ 挺有意思的



### 代码实现

```go
func maxTurbulenceSize(arr []int) int {
	n := len(arr)
	if n < 2 {
		return n
	}
	ans := 1
	count := 1
	prev := arr[1] - arr[0]
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	if prev != 0 {
		ans = 2
		count = 2
	}
	for r := 2; r < n; r++ {
		now := arr[r] - arr[r-1]
		if now != 0 && prev != 0 && prev^now < 0 {
			count++
			ans = max(count, ans)
			prev = now
			continue
		}
		if now != 0 {
			count = 2
			ans = max(ans, count)
		} else {
			count = 1
		}
		prev = now
	}
	return ans
}
```

