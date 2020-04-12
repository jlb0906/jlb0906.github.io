---
title: golang设计模式-简单工厂模式
date: 2020-04-12 23:25:46
tags:
---

简单工厂模式可以解决单体类过于庞大的问题

### 类图
![](/images/simple-factory.jpg)
<!-- more -->

### 定义Chart和实现工厂方法
```
package main

type Chart interface {
	Display()
}

func ChartFactory(t string) Chart {
	switch t {
	case "histogram":
		return NewHistogramChart()
	case "line":
		return NewLineChart()
	case "pie":
		return NewPieChart()
	}
	return nil
}
```

### 定义HistogramChart
```
package main

import "fmt"

type HistogramChart struct {}

func NewHistogramChart() *HistogramChart {
	fmt.Println("new NewHistogramChart")
	return &HistogramChart{}
}

func (h *HistogramChart) Display() {
	fmt.Println("display HistogramChart...")
}
```

### 定义LineChart
```
package main

import "fmt"

type LineChart struct {}

func NewLineChart() *LineChart {
	fmt.Println("new NewLineChart")
	return &LineChart{}
}

func (h *LineChart) Display() {
	fmt.Println("display LineChart...")
}
```

### 定义PieChart
```
package main

import "fmt"

type PieChart struct {}

func NewPieChart() *PieChart {
	fmt.Println("new NewPieChart")
	return &PieChart{}
}

func (h *PieChart) Display() {
	fmt.Println("display PieChart...")
}
```


### 客户端调用
```
package main

func main() {
	c := ChartFactory("pie")
	c.Display()
}
```

![](/images/simple-factory-client.PNG)