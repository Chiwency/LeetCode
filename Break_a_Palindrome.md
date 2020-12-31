## [破坏回文串](https://leetcode-cn.com/problems/break-a-palindrome/)

是道字符串题，算中等题里的简单题，虽然很容易想出怎么解，但是有一些特殊情况比较坑需要多考虑。这道题挂了3次才写出。

```go
func breakPalindrome(palindrome string) string {
	l := len(palindrome) / 2
	data := []byte(palindrome)
	flag := 0
	for i := 0; i < l; i++ {
		if data[i] != 'a' {
			data[i] = 'a'
			flag = 1
			break
		}
	}
	if flag != 0 {
		return string(data)
	}
	if l >= 1 {
		data[len(palindrome)-1] = 'b'
		return string(data)
	}

	return ""
}
```

