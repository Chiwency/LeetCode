## [交替位二进制数](https://leetcode-cn.com/problems/binary-number-with-alternating-bits/)

开始写位运算的题，这题也能用位运算操作符写



### 代码实现

```go
func hasAlternatingBits(n int) bool {
	pre := -1
	for n > 0 {
		if n%2 == pre {
			return false
		}
		pre = n % 2
		n /= 2
	}
	return true
}
```



