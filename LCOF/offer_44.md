## [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

刚拿到有点懵，但是这种一看就是和数学相关的，还是静下心来找规律

我是按每个数的占用的位数，来推到第n位的位数

实际面试的时候可能有点紧张，这题有点恶心



看精选题解都差不多



### 代码实现

```go
func findNthDigit(n int) int {
	if n <= 9 {
		return n
	}
	num := 9
	digit := 1
	n++
	var i int
	for i = 10; i < n; {
		num *= 10
		digit++
		i += num * digit
	}
	i -= num * digit
	n -= i
	r := n % digit

	if r == 0 {
		n = n/digit - 1 + num/9
		nByte := []byte(strconv.Itoa(n))
		return int(nByte[digit-1] - '0')
	}
	n = n/digit + num/9
	nByte := []byte(strconv.Itoa(n))
	return int(nByte[r-1] - '0')
}
```

