## [车队](https://leetcode-cn.com/problems/car-fleet/)

注意这种情况

> **10 **
>
> **[0,4,2] **
>
> **[2,1,3]**

就是靠终点的(前面的)车会限制后面的速度更快的车，导致后面的车速度会变，所以要先从最靠近终点的车开始判断，所以要先对位置进行排序。



### 代码实现

```go
func carFleet(target int, position []int, speed []int) int {
	fleet := make([]int, 0)
	l := len(position)
	hash := make(map[int]int)
	for i := 0; i < l; i++ {
		hash[position[i]] = speed[i]
	}
	sort.Ints(position)
	var t1 float32
	var t2 float32
	for i := l - 1; i >= 0; i-- {
		flag := true
		for _, v := range fleet {
			t1 = float32(target-v) / float32(hash[v])
			t2 = float32(target-position[i]) / float32(hash[position[i]])
			if (v <= position[i] && t2 >= t1) || (v >= position[i] && t2 <= t1) {
				flag = false
				break
			}
		}
		if flag {
			fleet = append(fleet, position[i])
		}
	}
	return len(fleet)
}
```

