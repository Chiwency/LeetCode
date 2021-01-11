## [字符串解码](https://leetcode-cn.com/problems/decode-string/)

一道栈的题。但是在做的过程中发现一个容易被忽视的问题，切片是指针类型，

代码里面用了`repeatCode:=stack[j+1]` 本质上还是用了`stack[]`的内存空间，所以如果`stack[]`变了，`repeatCode`也要变。 应该再给`repeatCode`单独申请一个空间 

**要注意下这个问题，debug搞了挺久**



### 代码实现

```go
func decodeString(s string) string {
	encode := []byte(s)
	l := len(encode)
	stack := make([]byte, 0)
	for i := 0; i < l; i++ {
		if encode[i] != ']' {
			stack = append(stack, encode[i])
			continue
		}
		// 找到要重复的编码
		j := len(stack) - 1
		for stack[j] != '[' {
			j--
		}
		repeatCode := make([]byte, 0)
		repeatCode = append(repeatCode, stack[j+1:]...)
		n := j - 1
		// 找到重复次数
		for n >= 0 && stack[n] >= '0' && stack[n] <= '9' {
			n--
		}
		kBtye := stack[n+1 : j]
		stack = stack[:n+1]
		k, _ := strconv.Atoi(string(kBtye))
		for m := 0; m < k; m++ {
			stack = append(stack, repeatCode...)
		}
	}
	return string(stack)
}
```

