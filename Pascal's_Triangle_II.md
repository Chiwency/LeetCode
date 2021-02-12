## [杨辉三角 II](https://leetcode-cn.com/problems/pascals-triangle-ii/)

本来以为有简单的数学公式，瞄了眼题解有递推二字，就想到可能要从第一行开始递推，时间没有限制的话也挺简单的



### 代码实现

```go
func getRow(rowIndex int) []int {
	if rowIndex == 0 {
		return []int{1}
	}
	ans := make([]int, rowIndex+1)
	ans[0], ans[1] = 1, 1
	for r := 2; r <= rowIndex; r++ {
		temp := make([]int, len(ans))
		copy(temp, ans)
		for i := 1; i < r; i++ {
			ans[i] = temp[i-1] + temp[i]
		}
		ans[r] = 1
	}
	return ans
}
```

