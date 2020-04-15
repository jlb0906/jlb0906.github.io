---
title: golang设计模式-单例模式
date: 2020-04-15 11:00:28
tags:
---

单例模式用于系统运行时只需一个实例的时候，可节省系统开支

### 类图
本例中实现一个饿汉式单例模式
![](/images/singleton.gif)
<!-- more -->

### 以实现一个负载均衡器为例
```
package main

type LoadBalancer interface {
	AddServer(string)
	GetServer() string
}

var lb LoadBalancer

type SimpleLoadBalancer struct {
	serverMap map[string]struct{}
}

func NewSimpleLoadBalancer() *SimpleLoadBalancer {
	m := make(map[string]struct{})
	return &SimpleLoadBalancer{serverMap: m}
}

func (s *SimpleLoadBalancer) AddServer(srv string) {
	s.serverMap[srv] = struct{}{}
}

func (s *SimpleLoadBalancer) GetServer() string {
	for srv := range s.serverMap {
		return srv
	}
	return ""
}

func GetLoadBalancer() LoadBalancer {
	return lb
}

func init() {
	lb = NewSimpleLoadBalancer()
}
```

### 客户端调用测试
```
package main

import "fmt"

func main() {
	lb := GetLoadBalancer()
	lb.AddServer("server 1")
	lb.AddServer("server 2")
	lb.AddServer("server 3")

	fmt.Println(lb.GetServer())
}
```
![](/images/singleton_client.PNG)

### 后记
本次实现中未考虑并发，实际运用时，需要考虑serverMap的并发访问
