## [矩阵置零](https://leetcode-cn.com/problems/set-matrix-zeroes/)

一开始看题目说可以用O(1)的空间复杂度解，就开始想一步登天了，完全想歪了，其实可以先想一下用额外的空间怎么解，然后就进一步发现可以利用矩阵空间，这样既缩减到O(1)的空间复杂度。

所以说，饭要一口一口吃，题要一步一步做



### 代码实现

```go
func setZeroes(matrix [][]int) {
   m := len(matrix)
   n := len(matrix[0])
   row := make([]bool, m)
   col := make([]bool, n)
   for i, v := range matrix {
      for j, x := range v {
         if x == 0 {
            row[i] = true
            col[j] = true
         }
      }
   }
   for i, v := range matrix {
      for j, _ := range v {
         if row[i] || col[j] {
            matrix[i][j] = 0
         }
      }
   }
   return
}
```