---
title: golang设计模式-装饰模式
date: 2020-04-27 14:22:14
tags:
---

装饰模式可以以统一的接口增强现有的类

### 类图，以窗口组件为例
![](/images/decorator.gif)
<!-- more -->

### 代码实现
```
package main

import "fmt"

type Component interface {
	Display()
}

type Window struct {
}

func NewWindow() *Window {
	return &Window{}
}

func (w *Window) Display() {
	fmt.Println("Display Window")
}

type TextBox struct {
}

func NewTextBox() *TextBox {
	return &TextBox{}
}

func (t *TextBox) Display() {
	fmt.Println("Display TextBox")
}

type ScrollBallDecorator struct {
	c Component
}

func NewScrollBallDecorator(c Component) *ScrollBallDecorator {
	return &ScrollBallDecorator{c: c}
}

func (s *ScrollBallDecorator) Display() {
	s.c.Display()
	s.SetScrollBall()
}

func (s *ScrollBallDecorator) SetScrollBall() {
	fmt.Println("Set Scroll Ball")
}

type BlackBorderDecorator struct {
	c Component
}

func NewBlackBorderDecorator(c Component) *BlackBorderDecorator {
	return &BlackBorderDecorator{c: c}
}

func (b *BlackBorderDecorator) Display() {
	b.c.Display()
	b.SetBlackBorder()
}

func (b *BlackBorderDecorator) SetBlackBorder() {
	fmt.Println("Set Black Border")
}
```

### 调用测试
```
package main

func main() {
	var c1, c2, c3 Component
	c1 = NewWindow()
	c2 = NewScrollBallDecorator(c1)
	c3 = NewBlackBorderDecorator(c2)
	c3.Display()
}
```

![](/images/decorator_client.PNG)