---
title: golang设计模式-原型模式
date: 2020-04-16 10:41:18
tags:
---

原型模式用于需要模板的时候，比如本例中的周报

### 类图
![](/images/prototype.gif)
<!-- more -->

### 代码展示
```
package main

import (
	"encoding/json"
	"fmt"
	"log"
)

type Attachment struct {
	Name string
}

func NewAttachment(name string) *Attachment {
	return &Attachment{Name: name}
}

func (a *Attachment) GetName() string {
	return a.Name
}

func (a *Attachment) SetName(name string) {
	a.Name = name
}

func (a *Attachment) Download() {
	fmt.Println("downloading...")
}

type WeekLog struct {
	Name    string
	Date    string
	Content string
	Attach  *Attachment
}

func NewWeekLog(name string, date string, content string, attach *Attachment) *WeekLog {
	return &WeekLog{Name: name, Date: date, Content: content, Attach: attach}
}

func (w *WeekLog) GetName() string {
	return w.Name
}

func (w *WeekLog) SetName(name string) {
	w.Name = name
}

func (w *WeekLog) GetDate() string {
	return w.Date
}

func (w *WeekLog) SetDate(d string) {
	w.Date = d
}

func (w *WeekLog) GetContent() string {
	return w.Date
}

func (w *WeekLog) SetContent(c string) {
	w.Content = c
}

func (w *WeekLog) GetAttach() *Attachment {
	return w.Attach
}

func (w *WeekLog) SetAttach(a *Attachment) {
	w.Attach = a
}

// deep clone
func (w *WeekLog) Clone() *WeekLog {
	data, err := json.Marshal(w)
	if err != nil {
		log.Fatal(err)
	}
	var c WeekLog
	json.Unmarshal(data, &c)
	return &c
}
```

### 客户端调用测试
```
package main

import "fmt"

func main() {
	log := NewWeekLog("my weeklog", "2020-4-16", "log log log", NewAttachment("my attachment"))
	fmt.Printf("[prototype]: %+v\n", log)
	clone := log.Clone()
	fmt.Printf("[clone]: %+v", clone)
}
```

![](/images/prototype_client.PNG)