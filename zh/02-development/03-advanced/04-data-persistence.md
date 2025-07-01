---
url: /zh/02-development/03-advanced/04-data-persistence.md
---
# 数据持久化

对于后台插件，数据应存储在插件目录下的 `data` 目录中。插件启动后，系统会自动将该目录挂载为可写。为了确保数据在插件重启后不会丢失，必须将所有数据存放在此目录下。如果数据存放在其他目录，插件重启后将无法恢复这些数据，从而导致数据丢失。

:::warning 警告
机器人断电后可能造成文件缓存数据丢失。建议在写入数据文件后调用 [sync](https://www.runoob.com/linux/linux-comm-sync.html) 命令，确保数据刷新到磁盘。
:::

示例代码：

```py
import os

os.system("sync")
```

## 数据操作建议

1. 本地文件存储：对于小型数据，推荐使用 JSON、SQLite 等文件存储方案。
2. 数据库存储：对于更复杂的数据需求，可以选择数据库进行持久化。
