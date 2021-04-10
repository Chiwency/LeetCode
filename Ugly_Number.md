## [丑数](https://leetcode-cn.com/problems/ugly-number/)

每日一题的简单题



### 代码实现

```go
func isUgly(n int) bool {
   if n <= 0 {
      return false
   }
   for n != 1 {
      if n%2 == 0 {
         n /= 2
      } else if n%3 == 0 {
         n /= 3
      } else if n%5 == 0 {
         n /= 5
      } else {
         return false
      }
   }
   return true
}
```