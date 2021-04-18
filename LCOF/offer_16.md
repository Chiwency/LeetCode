## [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

直接遍历算会超时，我就说怎么能这么简单。

发现超时才想到可以优化呀，，，把一个数对半分可以简化一半的计算量，一半又对半分，，，，，

用递归写也挺简单的



### 代码实现

```go
func myPow(x float64, n int) float64 {
	if n == 0 {
		return 1
	} else if n < 0 {
		return 1 / pow(x, -n)
	}
	return pow(x, n)
}

func pow(x float64, n int) float64 {
	if n == 0 {
		return 1
	} else if n == 1 {
		return x
	}
	temp := pow(x, n/2)
	if n%2 == 0 {
		return temp * temp
	}
	return temp * temp * x
}
```

