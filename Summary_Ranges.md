## [汇总区间](https://leetcode-cn.com/problems/summary-ranges/)

思路很容易想出来，但是一直在想怎么把代码写的简洁一点。

对比了下官方题解，发现不应该把两种情况给割裂开来，单元素也看成一个区间，应该先把左边界的值输进去

还是官方题解的代码更优雅，文末附上代码

### 代码实现

```go
func summaryRanges(nums []int) []string {
	first := 0
	last := 0
	result := make([]string, 0)
	nums = append(nums, math.MinInt64)
	l := len(nums)
	for i := 0; i < l; i++ {
		if i == 0 {
			first = nums[i]
			last = nums[i]
			continue
		}

		if nums[i]-last == 1 {
			last = nums[i]
			continue
		} else if first == last {
			result = append(result, strconv.Itoa(last))
		} else {
			result = append(result, strconv.Itoa(first)+"->"+strconv.Itoa(last))
		}
		first = nums[i]
		last = nums[i]

	}
	return result
}
```



> 附一张官方题解的代码

```go
func summaryRanges(nums []int) (ans []string) {
    for i, n := 0, len(nums); i < n; {
        left := i
        for i++; i < n && nums[i-1]+1 == nums[i]; i++ {
        }
        s := strconv.Itoa(nums[left])
        if left < i-1 {
            s += "->" + strconv.Itoa(nums[i-1])
        }
        ans = append(ans, s)
    }
    return
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/summary-ranges/solution/hui-zong-qu-jian-by-leetcode-solution-6zrs/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

