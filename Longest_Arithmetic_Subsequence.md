

## [最长等差数列](https://leetcode-cn.com/problems/longest-arithmetic-subsequence/)

这题差点没把我给送走，坑太多，挂了四次才做出来，，， 状态转移方程很容易想出，很自然想到需要用map

第一次发现可以把`map`放进切片

**踩了很多坑，比如复制`map`不能直接用`mapA=mapB` ，写了测试，发现map应该是引用类型，底层还是同一块内存，所以要复制`map`还是要`range`一遍，按元素一个个复制**

如果是`map`中不存在的`key`被引用，就是默认值，比如int类型是0

还有就是注意最后循环找最大值的时候可以合并在里面，减少时间复杂度，这个很容易被忽略

### 代码实现

```go
func longestArithSeqLength(A []int) int {
	l := len(A)
	dp := make([]map[int]int, l)
	initMap := make(map[int]int)
	dp[l-1] = initMap
    maxLength:=0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := l - 2; i >= 0; i-- {
		// dp[i]=dp[i+1]  注意这句是引用，本质上还是同一个内存空间，没有新增一个map
		dp[i] = make(map[int]int)
		for j := i + 1; j < l; j++ {
			step := A[i] - A[j]
			_, ok := dp[j][step]
			_, exist := dp[i][step]
			if !exist {
				dp[i][step] = 2
			}
			if ok {
				// dp[i][step] 如果不存在的话被引用就是默认值0
				dp[i][step] = max(dp[j][step]+1, dp[i][step])
			}
            // 在循环里面找最大，省得最后又要遍历一次
            if dp[i][step]>maxLength{
                maxLength=dp[i][step]
            }
		}
	}

	return maxLength
}
```

