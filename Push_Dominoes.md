## [推多米诺](https://leetcode-cn.com/problems/push-dominoes/)

假的动态规划，主要还是双指针，这是我写的迄今为止最丑的代码。实践证明，代码越丑，越复杂，越难debug。一开始没想到其他好解法，吐了.  

> 后来看官方题解的思路比较简单，整块整块思考，虽然总是那几种情况，但是整体思考比较有条理性，一看就懂
>
> 官方给的算法思想：
>
> + 如果我们有 "A....B"，当 A = B，那么就变成 "AAAAAA"。
> + 如果我们有 "R....L"，那么结果会变成 "RRRLLL" 或者 "RRR.LLL" 如果点的个数是奇数。如果初始标记的坐标是 i 和 j，我们可以检查距离 k-i 和 j-k 来决定位置 k 的形态是 'L'，'R' 还是 '.'。
> + 如果我们有 "L....R"，就什么都不做，跳过。
>
> 作者：LeetCode
> 链接：https://leetcode-cn.com/problems/push-dominoes/solution/tui-duo-mi-nuo-by-leetcode/
> 来源：力扣（LeetCode）
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

**另外发现针对字符串持续 `s+="string"` 会导致运行超时，看某个题解直接用`string(slice)` 化成字符串就能过，这点要注意.**

### 代码实现

> 自己的思路，官方思路没写

```go
func pushDominoes(dominoes string) string {
	l := len(dominoes)
	dominoes += "."
	dp := []byte(dominoes)

	for i := 0; i < l; {
		if dp[i] != '.' {
			i++
			continue
		}
		j := i + 1
		for ; j < l; j++ {
			if dp[j] != '.' {
				break
			}
		}
		j--
		for i <= j {
			if dp[j+1] == 'L' {
				if i == 0 || dp[i-1] == 'L' {
					dp[j] = dp[j+1]
					j--
				} else if dp[i-1] == 'R' {
					temp := dp[j-1]
					if dp[i+1] == 'L' {
						dp[i] = '.'
					} else {
						dp[i] = 'R'
					}
					if temp == 'R' {
						dp[j] = '.'
					} else {
						dp[j] = 'L'
					}
					i++
					j--
				}
			} else if i != 0 && dp[i-1] == 'R' {
				dp[i] = 'R'
				i++
			} else {
				i = j + 1
			}
		}
	}

	return string(dp[:l])
}
```

