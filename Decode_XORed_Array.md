## [解码异或后的数组](https://leetcode-cn.com/problems/decode-xored-array/)

异或运算的逆运算还是异或



### 代码实现

```go
func decode(encoded []int, first int) []int {
	l := len(encoded)
	ans := make([]int, l+1)
	ans[0] = first
	for i := 0; i < l; i++ {
		ans[i+1] = encoded[i] ^ first
		first = ans[i+1]
	}
	return ans
}
```

