## [救生艇](https://leetcode-cn.com/problems/boats-to-save-people/)

贪心算法  如果最重的一个和最轻的一个不能在一起，那么最重的一个独占一条船，然后右指针推进

但是一开始我想的是O(n2) 算法，后来又改进，超时了

> 超时算法： 排序，从左开始遍历，然后每次都要从又开始遍历找到最适合的那个胖一点的搭船，根本问题就是没想到可以先让胖的上船的，这样就不用每次都要从右开始遍历了



### 代码实现

```go
func numRescueBoats(people []int, limit int) int {
	sort.Ints(people)
	r := len(people) - 1
	sum, i := 0, 0
	for i <= r {
		if people[i]+people[r] <= limit {
			r--
			i++
		} else {
			r--
		}
		sum++
	}

	return sum
}
```

