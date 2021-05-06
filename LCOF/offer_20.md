## [剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

按逻辑硬解出来的，双百，但是错了N多次，，，，

看题解是用状态机做的，离谱，对状态机不熟，已经第二次碰到了，要好好看看



### 代码实现

```go
func isNumber(s string) bool {
	l, r := 0, len(s)-1
	for l <= r {
		if s[l] == ' ' {
			l++
		} else if s[r] == ' ' {
			r--
		} else {
			break
		}
	}
	s = s[l : r+1]
	for k, v := range s {
		if v == 'e' || v == 'E' {
			return (isInt(s[:k]) || isDemical(s[:k])) && isInt(s[k+1:])
		}
	}
	return isInt(s) || isDemical(s)
}

func isInt(s string) bool {
	if len(s) <= 0 {
		return false
	}
	hasNum := false
	for k, v := range s {
		if v == '+' || v == '-' {
			if k != 0 {
				return false
			}
			continue
		}
		if v > '9' || v < '0' {
			return false
		}
		hasNum = true
	}
	return hasNum
}

func isDemical(s string) bool {
	if len(s) <= 0 {
		return false
	}
	if s[0] == '+' || s[0] == '-' {
		s = s[1:]
	}
	flag := false
	hasNum := false
	for _, v := range s {
		if v == '.' {
			if flag {
				return false
			}
			flag = true
			continue
		}
		if v < '0' || v > '9' {
			return false
		}
		hasNum = true
	}
	return hasNum
}
```



