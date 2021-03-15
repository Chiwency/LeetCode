## [螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

不用额外空间不循环调用的话，只用循环写，需要注意的细节很多





### 代码实现

```go
func spiralOrder(matrix [][]int) []int {
	m := len(matrix)
	n := len(matrix[0])
	ans := make([]int, 0)
	c := 0
	for m > 0 && n > 0 && c < m && c < n {
		i, j := c, c
		for i < m && j < n {
			ans = append(ans, matrix[i][j])
			j++
		}
		if i == m-1 {
			return ans
		}
		j--
		i++
		for i < m && j < n {
			ans = append(ans, matrix[i][j])
			i++
		}
		if j == c {
			return ans
		}
		i--
		j--
		for j >= c && i >= c {
			ans = append(ans, matrix[i][j])
			j--
		}
		j++
		i--
		for i > c {
			ans = append(ans, matrix[i][j])
			i--
		}
		c++
		m--
		n--
	}
	return ans
}
```

