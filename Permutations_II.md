## [全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

同全排列一样的回溯算法，只是加了去重判断。

用`visit`哈希表记录访问过的数的下标，下标更大的相同的数定义成合法的，但是如果遇到下标更小的相同的数，就说明发生了重复，就舍弃.



### 代码实现

```go
func permuteUnique(nums []int) [][]int {
	visit := make(map[int]int)
	ans := make([][]int, 0)
	var dfs func(path []int)
	dfs = func(path []int) {
		if len(path) == len(nums) {
			temp := make([]int, len(path))
			copy(temp, path)
			ans = append(ans, temp)
			return
		}
		for k := range nums {
			v, ok := visit[nums[k]]
			if !ok {
				v = -1
			}
			if v < k {
				temp := v
				visit[nums[k]] = k
				path = append(path, nums[k])
				dfs(path)
				visit[nums[k]] = temp
				path = path[:len(path)-1]
			}
		}
	}
	dfs([]int{})
	return ans
}
```





