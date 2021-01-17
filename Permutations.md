## [全排列](https://leetcode-cn.com/problems/permutations/)

第一次开始刷回溯算法，其实和递归差不多

**注意`append`会另开一块内存，所以一般不要值传递切片然后又在调用函数里面用`append`函数，不然原内存的数据会丢失  是个坑**

**还有就是保存结果的适合要注意另开一个空间保存一个个结果，用同一个切片变量，会导致原来得到的结果被修改**

### 代码实现

```go
func permute(nums []int) [][]int {
	l := len(nums)
	result := make([][]int, 0)
	used := make(map[int]bool)
	var dfs func(path []int)
	dfs = func(path []int) {
		if len(path) == l {
            // path在后续会改变，因为切片是指针类型，所以要另起一块内存储存结果
			temp := make([]int, len(path))
			copy(temp, path)
			result = append(result, temp)
			return
		}
		for k := range nums {
			if !used[k] {
				path = append(path, nums[k])
				used[k] = true
				dfs(path)
				path = path[:len(path)-1]
				used[k] = false
			}
		}
	}
	dfs([]int{})
	return result
}
```

