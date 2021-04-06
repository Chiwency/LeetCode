## [ 删除有序数组中的重复项 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

双指针解法，看官方题解发现其实count也可以不要的，把count去掉代码可以更加简洁



### 代码实现

```go
func removeDuplicates(nums []int) int {
    l:=len(nums)
    count:=1
    i:=1
    for j:=1;j<l;j++{
        if nums[j]!=nums[i-1]{
            nums[i]=nums[j]
            count=1
            i++
            continue
        }
        if count<2{
            nums[i]=nums[j]
            count++
            i++
        }
    }
    return i
}
```

