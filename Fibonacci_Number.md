## [斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

正好碰到每日一题，水一波

### 代码实现

```go
func fib(n int) int {
	if n == 0 {
		return 0
	} else if n == 1 {
		return 1
	}
	return fib(n-1) + fib(n-2)
}
```

