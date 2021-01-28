## [组合总和](https://leetcode-cn.com/problems/combination-sum/)

回溯算法，有剪枝



### 代码实现

```go
func combinationSum(candidates []int, target int) [][]int {
	ans := make([][]int, 0)
	l := len(candidates)
	var dfs func(path []int, sum, n int)
	dfs = func(path []int, sum, n int) {
		if sum == target {
			temp := make([]int, len(path))
			copy(temp, path)
			ans = append(ans, temp)
			return
		} else if sum > target {
			return
		}
		for i := n; i < l; i++ {
			path = append(path, candidates[i])
			dfs(path, sum+candidates[i], i)
			path = path[:len(path)-1]
		}
	}
	sort.Ints(candidates)
	dfs([]int{}, 0, 0)
	return ans
}
```

