## [乘积小于K的子数组](https://leetcode-cn.com/problems/subarray-product-less-than-k/)

很容易能想到嵌套循环的O(n2)的解法，但这样设置成中等题就毫无意义

发现一丝丝不对劲 最后想到0(n)的解法，不过还是不够完美

看题解双指针解法，从右指针往前算，每移动一次右指针就算一次次数和 很巧妙，**避免了边界检查问题**

**要多学学题解的一些很巧的避免检查边界的技巧，经常会看到**



### 代码实现

```go
func numSubarrayProductLessThanK(nums []int, k int) int {
	nums = append(nums, 1)   // 为了检查边界，虽然看着很膈应，但是没办法
	n := len(nums)
	sum := 0
	product := 1
	l := 0
	for r := 0; r < n; r++ {
		product *= nums[r]
		for (product >= k || r == n-1) && l <= r {
			sum += r - l
			product /= nums[l]
			l++
		}
	}
	return sum
}
```



### 官方题解

> 很巧妙

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if (k <= 1) return 0;
        int prod = 1, ans = 0, left = 0;
        for (int right = 0; right < nums.length; right++) {
            prod *= nums[right];
            while (prod >= k) prod /= nums[left++];
            ans += right - left + 1;
        }
        return ans;
    }
}

作者：LeetCode
链接：https://leetcode-cn.com/problems/subarray-product-less-than-k/solution/cheng-ji-xiao-yu-kde-zi-shu-zu-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

