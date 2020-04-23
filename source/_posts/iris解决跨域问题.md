---
title: iris解决跨域问题
date: 2020-04-23 22:36:29
tags:
---

本来是参考官方的中间件跨域实现例子，但没有完全解决问题，Get请求可以跨域，Post怎么设置也不行。

后面参考(copy)了bbs-go这个开源项目的跨域代码，解决了这个很细节的问题。

### 代码实现
```
// cors
app.Use(cors.New(cors.Options{
    AllowedOrigins:   []string{"*"}, // allows everything, use that to change the hosts.
    AllowCredentials: true,
    MaxAge:           600,
    AllowedMethods:   []string{iris.MethodGet, iris.MethodPost, iris.MethodOptions, iris.MethodHead, iris.MethodDelete, iris.MethodPut},
    AllowedHeaders:   []string{"*"},
}))
app.AllowMethods(iris.MethodOptions)
```