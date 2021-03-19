## [设计停车系统](https://leetcode-cn.com/problems/design-parking-system/)

好简单,,,

### 代码实现

```go
type ParkingSystem struct {
	big    int
	medium int
	small  int
}

func Constructor(big int, medium int, small int) ParkingSystem {
	return ParkingSystem{big, medium, small}
}

func (this *ParkingSystem) AddCar(carType int) bool {
	switch carType {
	case 1:
		if this.big > 0 {
			this.big--
			return true
		}
	case 2:
		if this.medium > 0 {
			this.medium--
			return true
		}
	case 3:
		if this.small > 0 {
			this.small--
			return true
		}
	}
	return false
}

```

