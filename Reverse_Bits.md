## [颠倒二进制位](https://leetcode-cn.com/problems/reverse-bits/)

看题解发现我的解法还是不高效，位运算最好还是都用位运算解题 

答案的分治算法实现时间复杂度N(1)



### 代码实现

```go
func reverseBits(num uint32) uint32 {
    var a,ans uint32
    a=1<<31
    ans=0
    for i:=0;i<32;i++{
        if num&1==1{
            ans+=a
        }
        a>>=1
        num>>=1
    }
    return ans
}
```

