## [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一开始用map写，就知道不对劲，，但是想不出更好的

看了题解的位运算，真的是妙蛙种子吃了妙脆角妙到家了



### 代码实现

```go

func singleNumbers(nums []int) []int {
	n := 0
	for _, v := range nums {
		n ^= v
	}
	bit := 1
	for (n & bit) == 0 {
		bit <<= 1
	}
	a := 0
	b := 0
	for _, v := range nums {
		if v&bit == 0 {
			a ^= v
		} else {
			b ^= v
		}
	}
	return []int{a, b}
}
```

