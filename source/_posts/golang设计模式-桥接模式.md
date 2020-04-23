---
title: golang设计模式-桥接模式
date: 2020-04-23 18:22:59
tags:
---

桥接模式适用于类的多维度变化问题

### 类图，以照片显示类为例
![](/images/bridge.gif)
<!-- more -->

### 代码实现
```
package main

import "fmt"

type Image interface {
	SetImageImpl(impl ImageImpl)
	ParseFile()
}

type GifImage struct {
	impl ImageImpl
}

func (g *GifImage) SetImageImpl(i ImageImpl) {
	g.impl = i
}

func (g *GifImage) ParseFile() {
	fmt.Println("ParseFile of Gif")
	m := Matrix{}
	g.impl.DoPaint(m)
}

type PNGImage struct {
	impl ImageImpl
}

func (p *PNGImage) SetImageImpl(impl ImageImpl) {
	p.impl = impl
}

func (p *PNGImage) ParseFile() {
	fmt.Println("ParseFile of PNG")
	m := Matrix{}
	p.impl.DoPaint(m)
}
```

```
package main

import "fmt"

type Matrix struct {

}

type ImageImpl interface {
	DoPaint(Matrix)
}

type WindowsImageImpl struct {

}

func (w *WindowsImageImpl) DoPaint(matrix Matrix) {
	fmt.Print("在Windows上显示图像")
}

type LinuxImageImpl struct {

}

func (l *LinuxImageImpl) DoPaint(m Matrix) {
	fmt.Print("在Linux上显示图像")
}
```

### 客户端调用测试
```
package main

func main() {
	win := new(WindowsImageImpl)
	gif := new(GifImage)
	gif.SetImageImpl(win)
	gif.ParseFile()
}
```

![](/images/bridge_client.PNG)
