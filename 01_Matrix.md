## [01 矩阵](https://leetcode-cn.com/problems/01-matrix/)

一开始用深度优先搜索，一直超时，剪枝也不行，应该是递归的问题

后来看了题解的广度优先搜索，确实巧妙 学到了，学到了

BFS牛逼



### 代码实现

```go
func updateMatrix(matrix [][]int) [][]int {
	queue := make([][2]int, 0)
	length := len(matrix)
	width := len(matrix[0])
	ans := make([][]int, length)
	dirs := [][2]int{{-1, 0}, {1, 0}, {0, 1}, {0, -1}}
	for i := range matrix {
		ans[i] = make([]int, width)
		for j := range matrix[i] {
			if matrix[i][j] == 0 {
				queue = append(queue, [2]int{i, j})
				continue
			}
			ans[i][j] = -1
		}
	}

	for len(queue) != 0 {
		q := queue[0]
		queue = queue[1:]
		for d := 0; d < 4; d++ {
			i := q[0] + dirs[d][0]
			j := q[1] + dirs[d][1]
			if i >= 0 && i < length && j >= 0 && j < width && ans[i][j] == -1 {
				ans[i][j] = ans[q[0]][q[1]] + 1
				queue = append(queue, [2]int{i, j})
			}
		}
	}
	return ans
}
```

