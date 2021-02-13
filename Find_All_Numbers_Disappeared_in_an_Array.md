## [找到所有数组中消失的数字](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

这里是原地修改原数组，关键在于被定位位置上储存的值怎么保存下来，我是和索引值互换，然后继续往下定位，但是官方题解更妙一些，直接加一个数`n`，到时候再取模就能还原，同时还能区分有没有被定位过，真的很妙啊



### 代码实现

```go
func findDisappearedNumbers(nums []int) []int {
	l := len(nums)
	i := 0
	for i < l {
		if nums[i] != i+1 {
			temp := nums[i]
			nums[i], nums[temp-1] = nums[temp-1], nums[i]
		}
		if nums[i] == nums[nums[i]-1] {
			i++
		}
	}
	ans := make([]int, 0)
	for k := range nums {
		if nums[k] != k+1 {
			ans = append(ans, k+1)
		}
	}
	return ans
}
```

