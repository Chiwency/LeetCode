## [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

emmm好简单



### 代码实现

```go
func reverseLeftWords(s string, n int) string {
	b := []byte(s)
	return string(b[n:]) + string(b[:n])
}
```

