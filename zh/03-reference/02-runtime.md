---
url: /zh/03-reference/02-runtime.md
---
# 运行环境

后端插件运行在一个隔离的容器内，预装了Python3以及常用的pip包，可以通过界面上的`环境信息`按钮查看。

![](/images/reference/环境入口.png)

![](/images/reference/环境查看.png)

## 安装额外的pip包

插件系统支持安装额外的Python包来扩展运行环境的功能。为了保证系统安全性和稳定性，只支持安装预编译的wheel包（.whl文件）。

### 支持的包格式

* **仅支持wheel格式（.whl）**：wheel是Python的预编译二进制分发格式，安装速度快且避免了编译依赖问题
* **不支持源码包（.tar.gz）**：为了安全性考虑，系统禁止在线编译和下载依赖

### 安装方式

通过系统管理界面上传`.whl`文件：

![](/images/reference/安装whl.png)
