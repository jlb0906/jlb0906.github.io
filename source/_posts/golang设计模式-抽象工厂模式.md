---
title: golang设计模式-抽象工厂模式
date: 2020-04-14 13:18:13
tags:
---

抽象工厂模式可以用于生成一系列相关联的产品，解决工厂方法模式中工厂过多问题

### 类图
![](/images/abstract_factory.jpg)
<!-- more -->

### 定义产品：Button、TextField、ComboBox
```
package main

import "fmt"

type Button interface {
	Display()
}

type SpringButton struct {}

func (s *SpringButton) Display() {
	fmt.Println("i'm SpringButton...")
}

type SummerButton struct {}

func (s *SummerButton) Display() {
	fmt.Println("i'm SummerButton...")
}
```

```
package main

import "fmt"

type TextField interface {
	Display()
}

type SpringTextField struct {}

func (s *SpringTextField) Display() {
	fmt.Println("i'm SpringTextField...")
}

type SummerTextField struct {}

func (s *SummerTextField) Display() {
	fmt.Println("i'm SummerTextField...")
}
```

```
package main

import "fmt"

type ComboBox interface {
	Display()
}

type SpringComboBox struct {}

func (s *SpringComboBox) Display() {
	fmt.Println("i'm SpringComboBox...")
}

type SummerComboBox struct {}

func (s *SummerComboBox) Display() {
	fmt.Println("i'm SummerComboBox...")
}
```

### 定义抽象工厂
```
package main

import "fmt"

type SkinFactory interface {
	CreateButton() Button
	CreateTextField() TextField
	CreateComboBox() ComboBox
}

type SpringSkinFactory struct {
}

func (s *SpringSkinFactory) CreateButton() Button {
	fmt.Println("create spring style...")
	return new(SpringButton)
}

func (s *SpringSkinFactory) CreateTextField() TextField {
	fmt.Println("create spring style...")
	return new(SpringTextField)
}

func (s *SpringSkinFactory) CreateComboBox() ComboBox {
	fmt.Println("create spring style...")
	return new(SpringComboBox)
}

type SummerSkinFactory struct {
}

func (s *SummerSkinFactory) CreateButton() Button {
	fmt.Println("create summer style...")
	return new(SummerButton)
}

func (s *SummerSkinFactory) CreateTextField() TextField {
	fmt.Println("create summer style...")
	return new(SummerTextField)
}

func (s *SummerSkinFactory) CreateComboBox() ComboBox {
	fmt.Println("create summer style...")
	return new(SummerComboBox)
}
```

### 客户端调用测试
```
package main

func main() {
	f := new(SummerSkinFactory)
	b := f.CreateButton()
	b.Display()
}
```

![](/images/abstract_factory_client.PNG)