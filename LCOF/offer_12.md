## [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

广度优先(套皮的深度优先)+回溯  

精选题解也差不多，但是我时间，空间消耗咋这么高呢，好家伙，。。

在记录走过的路径上面，先临时修改broad的值，递归返回之后再修改回来

想到了原地修改值，但是怕破坏broad影响后面的递归，没想到递归后可以还原，好家伙，是我太菜了，，，



### 代码实现

```go
func exist(board [][]byte, word string) bool {
	if len(word) == 0 {
		return true
	}
	wordByte := []byte(word)
	path := make([][2]int, 1)
	for i, v := range board {
		for j := range v {
			if board[i][j] == word[0] {
				path[0] = [2]int{i, j}
				if bfs(board, wordByte[1:], path) {
					return true
				}
			}
		}
	}
	return false
}

func bfs(board [][]byte, word []byte, path [][2]int) bool {
	if len(word) <= 0 {
		return true
	}
	direction := [][]int{{1, 0}, {0, 1}, {0, -1}, {-1, 0}}
	for _, v := range direction {
		m := path[len(path)-1][0] + v[0]
		n := path[len(path)-1][1] + v[1]
		if m >= 0 && m < len(board) && n >= 0 && n < len(board[0]) && board[m][n] == word[0] {
			flag := true

			for _, val := range path {
				if m == val[0] && n == val[1] {
					flag = false
					break
				}
			}
			path = append(path, [2]int{m, n})
			if flag && bfs(board, word[1:], path) {
				return true
			}
			path = path[:len(path)-1]
		}
	}
	return false
}
```

