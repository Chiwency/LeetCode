## [视频拼接](https://leetcode-cn.com/problems/video-stitching/)

看题解比较巧妙，头一次见这种形式的状态转移方程

针对区间[0,T]起一个DP数组。 `dp[i]` 表示满足区间`[0,i]` 所用的最小片段数目

则状态转移方程为

```go
dp[i]=dp[l]+1     // 对某一片段 [l,r]  i落在l,r中间时，dp[l]为满足[0,l]的最小片段数
```



### 代码实现

```go
func videoStitching(clips [][]int, T int) int {
	const maxInt = math.MaxInt64 - 1
	dp := make([]int, T+1)
	for i := 1; i <= T; i++ {
		dp[i] = maxInt
	}
	for i := 1; i <= T; i++ {
		for _, v := range clips {
			l := v[0]
			r := v[1]
			if i > l && i <= r && dp[l]+1 < dp[i] {
				dp[i] = dp[l] + 1
			}
		}
	}
	if dp[T] == maxInt {
		return -1
	}
	return dp[T]
}
```



**一开始想到用贪心实现，用切片数组排序，但是看官方贪心也是枚举区间`[0,T]` 的值来动态更新。 这是一种新思路**



