## [飞机座位分配概率](https://leetcode-cn.com/problems/airplane-seat-assignment-probability/)

仔细想可以发现一个特点。对于`1 2 3 4 5 6`的序列， 如果`1`选了`4` 那么`(1,4)`就定下来了，这时候就相当于`4`是那个没有票的乘客，他本来应该坐上`1`的位置，但是又要从`1`和`(4,6]`中随机选，这样就可以开始套娃了。所以设`dp[i]`为乘客序列`[i-n]`中，最后一个乘客坐在自己座位上的概率.

可以很快的写出它的状态转移方程:

```go
for j:=i;j<n-1;j++{
    d:=n-i
	dp[i]+=dp[j+1]/d
}
```

### 第一步代码

> 根据上面的思路写出的代码如下

```go
func nthPersonGetsNthSeat(n int) float64 {
	dp := make([]float64, n)
	dp[n-1] = 1
	for i := n - 2; i >= 0; i-- {
		for j := i; j < n-1; j++ {
			d := n - i
			dp[i] += dp[j+1] / float64(d)
		}
	}
	return dp[0]
}
```

但是这个代码是O（n2）的复杂度提交超时了。所以要继续研究优化。可以发现`dp[i]`其实满足一个递推公式

`dp[i]=（dp[i+1]*(d-1)+dp[i+1]）/d` 实际上就是`dp[i]=dp[i+1]` 但是`i=n-1`有点特殊，`dp[n-1]=1`

因为这个递推公式本来就是在`n>2`时开始递推的

所以 可以得出：

### 推导结论

```go
if n == 1 {
    return 1
} else {
    return 0.5
}
```

