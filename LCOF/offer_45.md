## [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

之前写过这道题，现在再写还是和之前一样，先想的是补齐，用最后一位数，发现不行，又用第一位数，还是不行，最后看到题解才想到是循环补齐，第一次做的时候是想到了的，但是第二次做没想起来，，淦

还是挺简单的吧



### 代码实现

```go
func minNumber(nums []int) string {
	padNums := make([][2]int, len(nums))
	for k := range nums {
		padNums[k] = [2]int{pad(nums[k]), nums[k]}
	}
	sort.Slice(padNums, func(i, j int) bool {
		return padNums[i][0] < padNums[j][0]
	})
	ans := ""
	for _, v := range padNums {
		ans += strconv.Itoa(v[1])
	}
	return ans
}

func pad(num int) int {
	s := strconv.Itoa(num)
	i := 0
	for len(s) < 10 {
		s += string(s[i])
		i++
	}
	num, _ = strconv.Atoi(s)
	return num
}
```

