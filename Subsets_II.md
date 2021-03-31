## [子集 II](https://leetcode-cn.com/problems/subsets-ii/)

很明显的回溯，用回溯套路解



### 代码实现

```go
func subsetsWithDup(nums []int) [][]int {
	sort.Ints(nums)
	l := len(nums)
	ans := make([][]int, 0)
	var dfs func(path []int, i int)
	dfs = func(path []int, i int) {
		temp := make([]int, len(path))
		copy(temp, path)
		ans = append(ans, temp)
		for i < l {
			var n int
			for n = i; n < l; n++ {
				if n < l-1 && nums[n+1] == nums[n] {
					continue
				}
				break
			}
			for a := 0; a <= n-i; a++ {
				path = append(path, nums[i])
				dfs(path, n+1)
			}
			path = path[:len(path)-n+i-1]
			i = n + 1
		}
		return
	}
	dfs([]int{}, 0)
	return ans
}
```

