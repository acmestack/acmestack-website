---
title: "代码规范"
description: "代码规范"
lead: ""
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "contributing"
weight: 55
toc: true
---

- Go
  - [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
  - [Effective Go](https://golang.org/doc/effective_go.html)
  - 了解和避免 [Go landmines](https://gist.github.com/lavalamp/4bd23295a9f32706a48f)
  - 代码注释
    - [Go's commenting conventions](http://blog.golang.org/godoc-documenting-go-code)
    - 如果审查者询问这段代码为什么是这样，那么注释会非常有用。
    - 命令行标志应该使用破折号，而不是下划线
    - 命名
      - 选择接口名称时请考虑包名，避免冗余。 例如, `storage.Interface` 优于 `storage.StorageInterface`。
      - 不要在包名称中使用大写字符、下划线或破折号。
      - 选择包名时请考虑父目录名。 例如, `pkg/controllers/autoscaler/foo.go` 应该叫 `package autoscaler` 而不是 `package autoscalercontroller`。
          - 除非有充分的理由, `package foo` 行应该与 `.go` 文件所在目录的名称相匹配。
          - 如果需要消除歧义，引入者可以使用不同的名称。
      - 锁应该被称为 `lock` 并且永远不应该被嵌入 (always `lock sync.Mutex`). 当存在多个锁时，按照 Go 约定为每个锁指定一个不同的名称： `stateLock`, `mapLock` 等。
    - [API conventions]
    - [Logging conventions]

## 测试规范

  - 所有新包和重要的新功能都必须附带单元测试。
  - 表驱动测试是测试多个场景/输入的首选。
  - 不要期望异步的事情会立即发生——不要等待一秒钟就期望 pod 正在运行。请等待并重试。
  - 有关其他测试建议，请参阅 [测试指南](../testing-guide) 。

## 目录和文件规范

  - 避免包杂乱无章。为新包找到合适的子目录。
    - 没有合适主目录的包放入新的包子目录 `pkg/util`.
  - 避免使用通用的包. 名为“util”的包是没有明确含义的。相反，创建一个描述您所需功能的名称。 例如, 处理等待操作的实际函数在 `wait` 包中并包括类似的功能`Poll`。 全称是 `wait.Poll`。
  - 所有文件名都应为小写。
  - Go 源文件和目录使用下划线，而不是破折号。
    - 包目录通常应尽可能避免使用分隔符。当包名是多个单词时，它们通常应该在嵌套的子目录中。
  - 文档目录和文件名应该使用破折号而不是下划线。
  - 遵循第三方代码的这些约定：
    - 普通第三方依赖项的 Go 代码使用 [go modules](https://github.com/golang/go/wiki/Modules) 进行管理。
    - 其他第三方代码放入 `third_party`.
      - fork的第三方 Go 代码放入 `third_party/forked`.
      - forked 的goland标准库放入 `third_party/forked/golang`.
    - 第三方代码必须包含许可证。这也包括修改后的第三方代码和摘录。
