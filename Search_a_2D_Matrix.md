## [搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)

抽象成一维数组，用二分查找，比较简单。



### 代码实现

```go
func searchMatrix(matrix [][]int, target int) bool {
	m := len(matrix)
	n := len(matrix[0])
	for l, r := 0, m*n-1; l <= r; {
		mid := (l + r) / 2
		i := mid / n
		j := mid % n
		if matrix[i][j] > target {
			r = mid - 1
		} else if matrix[i][j] < target {
			l = mid + 1
		} else {
			return true
		}
	}
	return false
}
```

