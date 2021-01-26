## [最大数](https://leetcode-cn.com/problems/largest-number/)

一开始想到桶排序，但是发现数字位数最多可以到9位，很麻烦，就想可不可以填充，把他们都填充到同样的位数

然后由大到小排序，组合按这个顺序排序的原数

第一次是末尾填充 9，但是发现问题`18 1`，如果这两个数末尾填充9，那么得到的就是`118` 

第二次是末尾填充该数的最后一位，可以解决上面的问题，但是又发现`6563 65` 这个组合，会得到`656365` 但是正确答案应该是`656563` 所以也不行

最后才想到填充该数字，比如`65 `填充为`656565656565` , 这样才解决了问题

太坎坷了，，，，



### 代码实现

```go
func largestNumber(nums []int) string {
   array := make([][2]int, len(nums))
   for k, v := range nums {
      array[k] = [2]int{pad(v), v}
   }
   sort.Slice(array, func(i, j int) bool {
      return array[i][0] > array[j][0]
   })
   if array[0][1] == 0 {
      return "0"
   }
   ans := ""
   for _, v := range array {
      ans += strconv.Itoa(v[1])
   }
   return ans
}

func pad(a int) int {
   s := []byte(strconv.Itoa(a))
   l := len(s)
   for i := 0; i < 10-l; i++ {
      s = append(s, s[i])
   }
   ans, _ := strconv.Atoi(string(s))
   return ans
}
```