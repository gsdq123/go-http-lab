# Go HTTP Lab

Go HTTP 框架对照实验室

这是一个用于系统学习 Go Web/HTTP 开发的个人实践项目。

项目把同一组 HTTP 场景分别用 `net/http`、Chi、Gin、Echo、Fiber 和 Mizu 实现，通过可运行的小程序对比不同框架在路由、上下文、中间件、错误处理、响应输出、生命周期管理等方面的设计差异。

我整理这个仓库的目的不是做框架宣传，也不是单纯堆 API 示例，而是把每个主题拆成足够小的实验：先跑通代码，再理解一次请求从进入进程到返回响应之间到底发生了什么。

## 项目定位

这个仓库适合用来：

- 学习 Go 标准库 `net/http` 的基础执行模型
- 对比主流 Go HTTP 框架的处理流程和抽象边界
- 理解中间件、路由、上下文、错误处理和响应写入的真实控制流
- 为自己选择 Go Web 框架时建立更清晰的判断标准
- 把 Go 后端开发中常见 HTTP 能力拆开练习

这个仓库不追求：

- 大而全的业务项目模板
- 框架性能排行榜
- 复杂工程脚手架
- 只展示最终写法、不解释运行机制的速查手册

## 覆盖框架

| 框架 | 说明 |
| --- | --- |
| `net/http` | Go 标准库 HTTP 服务能力，也是理解其他框架的基础 |
| Chi | 基于 `net/http` 的轻量路由器，保留标准库处理模型 |
| Gin | 常用 Go HTTP 框架，使用框架上下文和统一辅助方法 |
| Echo | 使用返回 `error` 的 Handler 模型，强调集中错误处理 |
| Fiber | 基于 `fasthttp`，与 `net/http` 生态边界更明显 |
| Mizu | 基于 `net/http` 的框架，提供结构化上下文和错误处理 |

## 目录结构

每个编号目录都是一个独立主题。目录内通常包含：

- `README.md`：该主题的说明和代码讲解
- `nethttp/main.go`：标准库实现
- `chi/main.go`：Chi 实现
- `gin/main.go`：Gin 实现
- `echo/main.go`：Echo 实现
- `fiber/main.go`：Fiber 实现
- `mizu/main.go`：Mizu 实现

不同主题会根据框架支持情况略有差异，但整体组织方式保持一致，方便横向对比。

## 学习路线

建议按顺序阅读，也可以直接跳到感兴趣的主题。

| 目录 | 主题 | 说明 |
| --- | --- | --- |
| [01-hello-world](01-hello-world/README.md) | Hello World | 最小 HTTP 服务和请求响应流程 |
| [02-application](02-application/README.md) | 应用启动 | 应用对象、监听端口和服务启动方式 |
| [03-handler-signature](03-handler-signature/README.md) | Handler 签名 | 不同框架如何定义和调用处理函数 |
| [04-routing](04-routing/README.md) | 路由匹配 | 路径、方法和匹配规则 |
| [05-route-groups](05-route-groups/README.md) | 路由分组 | API 分组和公共前缀组织 |
| [06-middleware-chain](06-middleware-chain/README.md) | 中间件链 | 中间件包裹顺序和执行流程 |
| [07-short-circuit](07-short-circuit/README.md) | 提前返回 | 中间件或 Handler 如何中断后续流程 |
| [08-error-handling](08-error-handling/README.md) | 错误处理 | 普通错误、集中错误处理和 panic 恢复 |
| [09-request-input](09-request-input/README.md) | 请求输入 | Header、Query、Body 等输入读取 |
| [10-response-output](10-response-output/README.md) | 响应输出 | 状态码、Header 和响应体写入 |
| [11-json](11-json/README.md) | JSON | JSON 请求解析和响应输出 |
| [12-path-params](12-path-params/README.md) | 路径参数 | 动态路由参数读取 |
| [13-static-files](13-static-files/README.md) | 静态文件 | 静态资源和嵌入文件服务 |
| [14-templates](14-templates/README.md) | 模板渲染 | HTML 模板和服务端渲染 |
| [15-forms-upload](15-forms-upload/README.md) | 表单上传 | 表单字段和文件上传处理 |
| [16-websocket](16-websocket/README.md) | WebSocket | 长连接和双向通信 |
| [17-sse](17-sse/README.md) | SSE | Server-Sent Events 服务端推送 |
| [18-context-cancel](18-context-cancel/README.md) | Context 取消 | 请求取消、超时和资源释放 |
| [19-shutdown](19-shutdown/README.md) | 优雅关闭 | 服务停止和连接清理 |
| [20-logging](20-logging/README.md) | 日志 | 请求日志和处理链观测 |
| [21-metrics-tracing](21-metrics-tracing/README.md) | 指标与追踪 | 基础观测能力 |
| [22-testing](22-testing/README.md) | 测试 | Handler 和路由测试 |
| [23-performance](23-performance/README.md) | 性能考虑 | 框架性能相关的设计差异 |
| [24-interop](24-interop/README.md) | 互操作 | 与 `net/http` Handler 和中间件协作 |
| [25-tradeoffs](25-tradeoffs/README.md) | 框架取舍 | 如何从控制权、生态和复杂度判断框架 |

## 运行示例

进入任意主题下的框架目录后运行：

```bash
go run .
```

例如运行 Gin 版本的 Hello World：

```bash
cd 01-hello-world/gin
go run .
```

服务默认监听 `:8080`，可以用浏览器或 `curl` 访问：

```bash
curl http://localhost:8080/
```

## 常用命令

根目录提供了 `Makefile` 和若干脚本，用来生成整本 Markdown、同步 workspace、构建和做 smoke test。

```bash
make help
```

常用目标：

```bash
make book
make check
make clean
```

说明：

- `make book`：根据根 README 和各主题 README 生成 `BOOK.md`
- `make check`：抽取 README 中的代码、同步 Go workspace、构建并运行 smoke test
- `make clean`：清理生成文件

## 项目特点

这个项目的写法遵循几个原则：

- 同一主题尽量在不同框架中保持相同业务行为
- 每个示例都可以直接运行
- README 不只贴代码，也解释请求处理过程
- 尽量减少隐藏工具和额外封装
- 用横向对照帮助理解框架差异

相比只看单个框架文档，这种方式更容易看清：

- 哪些能力来自 Go 标准库
- 哪些能力由框架额外提供
- 框架在什么时候接管控制流
- Handler 是否直接持有 `http.ResponseWriter` 和 `*http.Request`
- 错误处理是分散在 Handler 内，还是交给框架集中处理
- 框架是否仍然属于 `net/http` 生态

## 适合谁看

这个仓库主要面向：

- 正在学习 Go 后端开发的人
- 想从 `net/http` 过渡到 Web 框架的人
- 想比较 Gin、Echo、Fiber、Chi 等框架差异的人
- 希望理解 HTTP 服务运行机制，而不只是复制代码的人
- 需要为项目选型 Go Web 框架的人

## GitHub About 建议

如果要设置 GitHub 仓库右侧的 About 描述，可以使用：

> Go HTTP Lab：用同一组示例横向比较 net/http、Chi、Gin、Echo、Fiber 和 Mizu，理解路由、中间件、上下文、错误处理、响应输出和服务生命周期。

推荐 Topics：

```text
go
golang
http
web-framework
net-http
gin
echo
fiber
chi
middleware
backend
learning
```

## 说明

这是我基于 Go HTTP 框架学习和实践整理的个人项目。仓库内容会随着学习过程持续调整，重点放在可运行示例、执行流程解释和框架设计取舍上。
