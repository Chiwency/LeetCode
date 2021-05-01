## [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

一开始想的是位运算，但是位运算又貌似没啥精妙的解法

看了下题解才看到原地置换，淦，一开始怎么没想到

之前做这种重复的题都是用位运算，被位运算带偏了



### 代码实现

```go
func findRepeatNumber(nums []int) int {
	for i := 0; i < len(nums); i++ {
		v := nums[i]
		if v == i {
			continue
		}
		if v == nums[v] {
			return v
		}
		nums[i], nums[v] = nums[v], nums[i]
		i--
	}
	return 0
}
```

