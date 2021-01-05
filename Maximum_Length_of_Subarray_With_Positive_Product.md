## [乘积为正数的最长子数组长度](https://leetcode-cn.com/problems/maximum-length-of-subarray-with-positive-product/)

遍历一遍，记录第一个负数的位置和最后一个负数的位置，如果最后子串积是负数的话可以剪去任一端使子串长最大，遇到0就重置

要注意不要真的用乘法，数一多就会溢出  遍历过程中记录负数的数量，据此判断乘积正负

### 代码实现

```go
func getMaxLen(nums []int) int {
	l := len(nums)
	first := 0
	last := 0
	negtive := 0
	count := 0
	result := 0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := 0; i < l; i++ {
		if nums[i] != 0 {
			count++
		}
		if nums[i] < 0 {
			if first == 0 {
				first = count
			}
			last = count
			negtive++
		}

		if nums[i] == 0 || i == l-1 {
			if negtive%2 != 0 {
				count = max(count-first, last-1)
				result = max(result, count)
			} else {
				result = max(result, count)
			}
			negtive = 0
			count = 0
			first = 0
			last = 0
		}
	}

	return result
}
```

