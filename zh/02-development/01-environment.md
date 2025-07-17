---
url: /zh/02-development/01-environment.md
---
# 开发环境搭建

插件开发需要依赖适当的开发环境，例如Node.js、Python。

## VSCode下载、安装

1. 下载VSCode安装文件

在官方网站：https://code.visualstudio.com/

下载最新版本的 VSCode 即可

![](/images/development/下载vsc.png)

2. 下载完成单击运行，按照提示安装即可

![](/images/development/安装vsc.png)

## VSCode插件安装

1. 在VSCode插件市场中搜索 [Agilebot Extension Helper](https://marketplace.visualstudio.com/items?itemName=agilebot.vscode-agilebot-extension-helper) 进行安装

![](/images/development/安装vsc插件.png)

## Node.js下载、安装

1. 下载nvm安装文件

在GitHub: https://github.com/coreybutler/nvm-windows/releases

下载nvm-setup.exe即可

![](/images/development/下载nvm.png)

2. 下载完成单击运行，按照提示安装即可

![](/images/development/安装nvm1.png)

3. 安装完成后在终端输入 `nvm -v`，能查到版本号，说明安装成功了

![](/images/development/安装nvm2.png)

4. 设置nvm镜像源，在终端输入以下命令

```bash
nvm node_mirror https://npmmirror.com/mirrors/node/
```

5. 使用nvm安装node，在终端输入以下命令

```bash
nvm install 20
nvm use 20
```

![](/images/development/安装nvm3.png)

6. 安装完成后在终端输入`node -v`，能查到版本号，说明安装成功了

![](/images/development/安装nvm4.png)

7. 设置node镜像源，在终端输入以下命令

```bash
npm config set registry https://registry.npmmirror.com
```

8. 启用corepack，在终端输入以下命令

```bash
corepack enable
```

9. 设置corepack镜像源，在系统设置中设置如下环境变量

```bash
COREPACK_NPM_REGISTRY=https://registry.npmmirror.com
```

![](/images/development/配置corepack.png)

## Python下载、安装

1. 下载Python安装文件

在官方网站：https://www.python.org/downloads/windows/

下载最新版本的 Python 即可

![](/images/development/下载py.png)

2. 下载完成单击运行，按照提示安装即可
