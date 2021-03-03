## [1比特与2比特字符](https://leetcode-cn.com/problems/1-bit-and-2-bit-characters/)

还挺简单



### 代码实现

```go
func isOneBitCharacter(bits []int) bool {
	flag := 0
	for i := 0; i < len(bits); i++ {
		if bits[i] == 0 {
			flag = 0
		} else {
			i++
			flag = 1
		}
	}
	return flag == 0
}
```

