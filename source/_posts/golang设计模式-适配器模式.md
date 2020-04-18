---
title: golang设计模式-适配器模式
date: 2020-04-18 10:01:56
tags:
---

适配器模式解决接口不一致的问题

### 类图，以分数操作为例
![](/images/adapter.jpg)
<!-- more -->

### 实现
```
package main

type ScoreOperation interface {
	Sort([]int) []int
	Search([]int, int) int
}

type OperationAdapter struct {
}

func (o *OperationAdapter) Sort(a []int) []int {
	return quickSort(a)
}

func (o *OperationAdapter) Search(a []int, k int) int {
	return binarySearch(a, k)
}
```

```
package main

func quickSort(arr []int) []int {
	sort(arr, 0, len(arr)-1)
	return arr
}

func sort(arr []int, p, r int) {
	q := 0
	if p < r {
		q = partition(arr, p, r)
		sort(arr, p, q-1)
		sort(arr, q+1, r)
	}
}

func partition(arr []int, p, r int) int {
	x := arr[r]
	j := p - 1

	for i := p; i <= r-1; i++ {
		if arr[i] <= x {
			j++
			swap(arr, j, i)
		}
	}
	swap(arr, j+1, r)
	return j + 1
}

func swap(arr []int, x, y int) {
	t := arr[x]
	arr[x] = arr[y]
	arr[y] = t
}

func binarySearch(arr []int, key int) int {
	low := 0
	high := len(arr) - 1
	for low <= high {
		mid := (low + high) / 2
		midVal := arr[mid]
		if midVal < key {
			low = mid + 1
		} else if midVal > key {
			high = mid - 1
		} else {
			return 1 //找到元素返回1
		}
	}
	return -1 //未找到元素返回-1
}
```

### 调用测试
```
package main

import "fmt"

func main() {
	var o ScoreOperation
	o = new(OperationAdapter)
	a := []int{1, 3, 2}
	fmt.Printf("before sort: %v\n", a)
	o.Sort(a)
	fmt.Printf("after sort: %v\n", a)
}
```

![](/images/adapter_client.PNG)