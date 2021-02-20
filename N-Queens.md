## [ N 皇后](https://leetcode-cn.com/problems/n-queens/)

其实不是很难，用通用的回溯算法解就可，只要处理好怎么判断同一行、列、和两条斜线上是否有棋子就可。



### 代码实现

```go
func solveNQueens(n int) [][]string {
	ans := make([][]string, 0)
	// 反向操作，visit 下标代表列,元素代表行
	visit := make([]int, n)
	for k := range visit {
		visit[k] = -1
	}
	fill := func(index int) (ans string) {
		for i := 0; i < n; i++ {
			if i == index {
				ans += "Q"
			} else {
				ans += "."
			}
		}
		return
	}
	var dfs func(path []string, depth int)
	dfs = func(path []string, depth int) {
		if depth == n {
			temp := make([]string, len(path))
			copy(temp, path)
			ans = append(ans, temp)
		}
		for i := 0; i < n; i++ {
			// 该列没棋子才能进一步判断
			if visit[i] < 0 {
				flag := true
				// 判断斜对角有没有棋子，有左上和右上两个方向
				for j := 0; j < depth; j++ {
					sub := depth - j
					l := i - sub
					r := i + sub
					if (l >= 0 && visit[l] == depth-sub) || 
                    (r < n && visit[r] == depth-sub) {
						flag = false
						break
					}
				}
				if flag {
					path = append(path, fill(i))
					visit[i] = depth
					dfs(path, depth+1)
					visit[i] = -1
					path = path[:len(path)-1]
				}
			}
		}
	}

	dfs([]string{}, 0)
	return ans
}
```

