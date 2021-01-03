## [三数之和](https://leetcode-cn.com/problems/3sum/)

固定第一个，移动后两个进行匹配 顺序是 `nums[i] nums[l] nums[r]`  

然后把第一个移动一位继续上一步

注意答案要去重，比如`1 1 2 3` 遍历的时候就要跳过重复的1. 



### 代码实现

```go
func threeSum(nums []int) [][]int {
	sort.Ints(nums)
	result := make([][]int, 0)
	n := len(nums)
	for i := 0; i < n-2; i++ {
		if nums[i] > 0 {
			break
		}
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}
		l := i + 1
		r := n - 1
		for l < r {
			if l > i+1 && nums[l] == nums[l-1] {
				l++
				continue
			} else if r < n-1 && nums[r] == nums[r+1] {
				r--
				continue
			}
			sum := nums[i] + nums[l] + nums[r]
			if sum == 0 {
				result = append(result, []int{nums[i], nums[l], nums[r]})
				l++
				r--
			} else if sum > 0 {
				r--
			} else {
				l++
			}
		}
	}
	return result
}
```

