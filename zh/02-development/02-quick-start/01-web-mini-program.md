---
url: /zh/02-development/02-quick-start/01-web-mini-program.md
---
# Web小程序开发

> 该页面旨在指导开发者如何开发Web小程序类型的插件包。

## 关于Web小程序

### Web小程序是什么

Web小程序是指开发者根据自己的需求，在符合web开发规范的情况下，开发出的除AgileLink内已有页面之外的其他页面。

## 创建Web小程序

目前我们提供使用标准前端工程来创建一个Web小程序，在此处的示范中，我们会创建一个Web小程序类型的插件，该插件的功能是在页面显示“Hello Agilebot!”。

### 步骤一：创建插件文件夹

首先我们需要创建一份插件基本文件夹，该文件夹需包含一个config.json配置文件和前端工程文件，我们建议使用 src 作为前端工程的文件夹名称。

您可以从头开始手动创建，也可以使用插件开发包仓库中 ["demo"](https://github.com/sh-agilebot/extension-toolkit/tree/master/demo/HelloAgilebot) 目录下的模板进行修改。

:::tip 提示
下文中的 HelloAgilebot 就是我们即将创建的Web小程序的插件名。
:::

目录结构:

```ultree
output: simple
HelloAgilebot
  config.json
  src
    index.html
```

```html [index.html]
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello Agilebot!</title>
  </head>
  <body style="background-color:#f5f6fa;">
    <p style="font-size: 10vh;text-align: center;margin-top: 20%;">
      Hello Agilebot!
    </p>
  </body>
</html>
```

```json [config.json]
{
  "name": "HelloAgilebot",
  "type": "webMiniProgram",
  "description": "显示 Hello Agilebot!",
  "version": "0.1",
  "url": "index.html"
}
```

### 步骤二：打包、安装

插件打包请参考[打包与安装](../04-package)

### 步骤三：访问页面

下面将介绍两种方式访问之前制作的页面。

* 方法1：在插件管理中找到插件名，点击指南针按钮访问。

![](/images/development/小程序入口1.png)

![](/images/development/小程序展示1.png)

* 方法2：在`应用-Extension`菜单中，找到插件名，点击可访问。

![](/images/development/小程序入口2.png)

![](/images/development/小程序展示2.png)
