## 四数之和

和三数之和类似，先定住前两个，后两个再设置左右指针移动，然后注意去重



### 代码实现

```go
func fourSum(nums []int, target int) [][]int {
	n := len(nums)
	result := make([][]int, 0)
	sort.Ints(nums)
	for i := 0; i < n-3; i++ {
		if i > 0 && nums[i] == nums[i-1] {
			continue
		}
		for j := i + 1; j < n-2; j++ {
			if j > i+1 && nums[j-1] == nums[j] {
				continue
			}
			l := j + 1
			r := n - 1
			for l < r {
				if l > j+1 && nums[l] == nums[l-1] {
					l++
					continue
				} else if r < n-1 && nums[r] == nums[r+1] {
					r--
					continue
				}
				sum := nums[i] + nums[j] + nums[l] + nums[r]
				if sum == target {
					result = append(result, []int{nums[i], nums[j], nums[l], nums[r]})
					l++
					r--
				} else if sum > target {
					r--
				} else {
					l++
				}
			}
		}
	}
	return result
}
```

