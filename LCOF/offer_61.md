## [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

判断最大值和最小值的差，差值不应大于4  

但是对重复元素的判断错误，后来用hash去重





### 代码实现

```go
func isStraight(nums []int) bool {
	king := 0
	min := 14
	max := 0
	dict := make(map[int]bool)
	for _, v := range nums {
		if v == 0 {
			king++
			continue
		}
		if dict[v] {
			return false
		}
		dict[v] = true
		if v > max {
			max = v
		}
		if v < min {
			min = v
		}
	}
	return max-min <= 4 && 4-max+min <= king
}
```

