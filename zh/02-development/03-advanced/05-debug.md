---
url: /zh/02-development/03-advanced/05-debug.md
---
# 调试指南

## 日志

对于后台插件（简单服务、通用服务），可以在插件管理界面中查看插件运行时的日志信息。

### 简单服务

仅当使用 `globals` 中提供的 `logger` 打印日志时，日志内容才会出现在插件管理界面中：

```py
logger = globals().get('logger')

logger.info("这是一条日志")
```

### 通用服务

通用服务可以使用任意日志库（如 `logging`、`loguru` 等）进行日志输出，插件管理界面同样支持展示。

> 以下是插件管理界面中日志展示的截图：

![](/images/development/服务日志查看1.png)

![](/images/development/服务日志查看2.png)

## 在线编辑

所有插件类型都支持在线编辑，允许用户直接在插件管理界面中修改插件代码，并保存更改。

![](/images/development/在线编辑1.png)

点击“保存”按钮后，后台服务将自动重启以应用更新内容。

![](/images/development/在线编辑2.png)
