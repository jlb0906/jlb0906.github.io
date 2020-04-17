---
title: golang设计模式-建造者模式
date: 2020-04-17 19:14:13
tags:
---

该模式作用于产品的生产过程

### 本例以生产一个游戏角色为例， 类图
![](/images/builder.gif)
<!-- more -->

### 实现
```
package main

type Actor struct {
	Type string
	Sex string
	Face string
}

func (a *Actor) SetType(t string) {
	a.Type = t
}

func (a *Actor) GetType() string {
	return a.Type
}

func (a *Actor) SetSex(s string) {
	a.Sex = s
}

func (a *Actor) GetSex() string {
	return a.Sex
}

func (a *Actor) SetFace(f string) {
	a.Face = f
}

func (a *Actor) GetFace() string {
	return a.Face
}
```

```
package main

type ActorBuilder interface {
	BuildType()
	BuildSex()
	BuildFace()
	CreateActor() *Actor
}

type HeroBuilder struct {
	actor *Actor
}

func NewHeroBuilder() *HeroBuilder {
	return &HeroBuilder{actor: new(Actor)}
}

func (h *HeroBuilder) CreateActor() *Actor {
	return h.actor
}

func (h *HeroBuilder) BuildType() {
	h.actor.SetType("Hero")
}

func (h *HeroBuilder) BuildSex() {
	h.actor.SetSex("Male")
}

func (h *HeroBuilder) BuildFace() {
	h.actor.SetFace("Cool")
}

type AngleBuilder struct {
	actor *Actor
}

func NewAngleBuilder() *AngleBuilder {
	return &AngleBuilder{actor: new(Actor)}
}

func (a *AngleBuilder) BuildType() {
	a.actor.SetType("Angle")

}

func (a *AngleBuilder) BuildSex() {
	a.actor.SetSex("Female")

}

func (a *AngleBuilder) BuildFace() {
	a.actor.SetFace("mystical")
}

func (a *AngleBuilder) CreateActor() *Actor {
	return a.actor
}
```

```
package main

type ActorController struct {
}

func (a *ActorController) construct(b ActorBuilder) *Actor {
	b.BuildType()
	b.BuildSex()
	b.BuildFace()
	return b.CreateActor()
}
```

### 客户端调用测试
```package main

import "fmt"

func main() {
	b := NewAngleBuilder()
	c := new(ActorController)
	actor := c.construct(b)
	fmt.Printf("my face is %v", actor.Face)
}
```

![](/images/builder_client.PNG)