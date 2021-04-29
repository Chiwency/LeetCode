## [剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

符号位和数字都放在一个循环里判断了，所以有点丑

遍历一次，溢出用位运算判断，也挺简单的





### 代码实现

```go
func strToInt(str string) int {
	sign := 1
	num := 0
	s := []byte(str)
	flag := true
	for _, v := range s {
		if flag {
			switch {
			case v == ' ':
			case v == '+':
				flag = false
			case v == '-':
				sign = -1
				flag = false
			case v >= '0' && v <= '9':
				num = num*10 + int(v-'0')
				flag = false
			default:
				return 0
			}
		} else {
			if v >= '0' && v <= '9' {
				num = num*10 + int(v-'0')
				if (num>>31)&-1 > 0 {
					if sign > 0 {
						return math.MaxInt32
					}
					return math.MinInt32
				}
			} else {
				break
			}
		}
	}
	return sign * num
}
```

