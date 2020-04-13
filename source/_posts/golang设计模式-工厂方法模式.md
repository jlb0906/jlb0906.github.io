---
title: golang设计模式-工厂方法模式
date: 2020-04-13 20:17:17
tags:
---


工厂方法模式可以解决简单工厂模式中频繁修改工厂类的问题

### 类图
![](/images/factory_method.jpg)
<!-- more -->

### 创建Logger接口
```
package main

type Logger interface {
	WriteLog()
}
```

### 实现FileLogger和DatabaseLogger
```
package main

import "fmt"

type FileLogger struct {}

func NewFileLogger() *FileLogger {
	return &FileLogger{}
}

func (f *FileLogger) WriteLog() {
	fmt.Println("i'm write log to file...")
}
```

```
package main

import "fmt"

type DatabaseLogger struct {}

func NewDatabaseLogger() *DatabaseLogger {
	return &DatabaseLogger{}
}

func (f *DatabaseLogger) WriteLog() {
	fmt.Println("i'm write log to database...")
}
```

### 定义LoggerFactory接口
```
package main

type LoggerFactory interface {
	CreateLogger() Logger
}

```

### 实现FileLoggerFactory和DatabaseLoggerFactory
```
package main

import "fmt"

type FileLoggerFactory struct{}

func NewFileLoggerFactory() *FileLoggerFactory {
	return &FileLoggerFactory{}
}

func (f *FileLoggerFactory) CreateLogger() Logger {
	fmt.Println("i'm open file...")
	return NewFileLogger()
}

```

```
package main

import "fmt"

type DatabaseLoggerFactory struct{}

func NewDatabaseLoggerFactory() *DatabaseLoggerFactory {
	return &DatabaseLoggerFactory{}
}

func (f *DatabaseLoggerFactory) CreateLogger() Logger {
	fmt.Println("i'm open database...")
	return NewDatabaseLogger()
}

```

### 客户端调用测试
```
package main

func main() {
	f := NewDatabaseLoggerFactory()
	logger := f.CreateLogger()
	logger.WriteLog()
}

```

![](/images/factory_method_client.PNG)


### 讨论
是否在golang中有更加轻便的实现？