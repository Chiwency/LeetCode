## [只有两个键的键盘](https://leetcode-cn.com/problems/2-keys-keyboard/)

这道题主要是要先想出数学关系。一开始我想到只要是奇数就不行，要一个个粘贴，但是发现`9=3*3` 可以少一步，所以就发现应该是质数不行，只有质数才需要一个个粘贴。这里打上了动态规划的标签，所以很自然的想到用dp数组解决

> 实际上是被带坑里了，不需要用动态规划的，直接对n进行迭代计算，比动态规划更节省时间和空间。
>
> 

### 代码实现

```go
func minSteps(n int) int {
	dp:=make([]int,n+1)
	dp[1]=0
	for i:=2;i<=n;i++{
		dp[i]=i   // 质数的操作次数为该质数值,非质数的后面再改
		for j:=2;j*j<=i;j++{
			if i%j==0{
				dp[i]=dp[i/j]+j
				break
			}
		}
	}
	return dp[n]
}
```

