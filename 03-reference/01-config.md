---
url: /03-reference/01-config.md
---
# 配置文件

## 文件命名

固定为`config.json`。

## 文件内容

一个典型的插件配置文件如下所示：

```json [config.json]
{
  "name": "MyExtension",
  "author": "Your Name",
  "type": "generalService",
  "scriptLang": "python",
  "description": "My Demo Extension",
  "version": "1.0",
  "entry": "app.py",
  "url": ""
}
```

## 字段说明

### `name`

插件名称，作为插件的唯一标识。建议使用英文，并确保该名称在插件系统中是唯一的。

* 类型：string
* 示例："MyExtension"

### `author`

插件作者的姓名或团队名。

* 类型：string
* 示例："agilebot"

### `type`

插件类型，指定插件的功能类别。包括：

* "generalService"：通用服务插件。

* "easyService"：简单服务插件

* "webMiniProgram"：Web小程序插件

* 类型：string

* 示例："generalService"

### `scriptLang`

插件所使用的编程语言。目前只支持：

* "python"

### `description`

插件的简短描述，帮助用户了解插件的功能和用途。

* 类型：string
* 示例："My Demo Extension"

### `version`

插件的版本号，建议采用常见的语义化版本控制（SemVer）格式：`主版本号.次版本号.修订号`。

* 类型：string
* 示例："1.0"

### `entry`

通用服务插件的入口文件，这通常是一个 Python 脚本文件。

* 类型：string
* 示例："app.py"

### `url`

Web页面的入口文件，适合`Web小程序`或`通用服务`，这通常是一个 html 网页文件或网页路由地址。

* 类型：string
* 示例："index.html"

## 智能提示

我们使用 JSON Schema 来规范插件的配置文件格式。通过 JSON Schema，您可以明确指定插件配置的结构、字段类型、必填项等信息，确保插件的配置文件符合规范。这使得插件的开发和安装过程更加简单和可靠。

您可以通过包管理工具来安装JSON Schema：

::: code-group

```sh [npm]
npm install @agilebot/extension-schemas
```

```sh [yarn]
yarn add @agilebot/extension-schemas
```

```sh [pnpm]
pnpm add @agilebot/extension-schemas
```

:::

安装之后，您可以在项目中引用该插件的配置文件：

```json [config.json]
{
  "$schema": "./node_modules/@agilebot/extension-schemas/v1.0/extension-schema.json"
}
```

也可以使用unpkg CDN进行引用，如下所示：

```json [config.json]
{
  "$schema": "https://unpkg.com/@agilebot/extension-schemas/v1.0/extension-schema.json"
}
```
