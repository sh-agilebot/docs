---
url: /zh/02-development/02-quick-start/02-easy-service.md
---
# 简单服务开发

> 该页面旨在指导开发者如何开发简单服务类型的插件包。

## 关于简单服务

简单服务实际是1个 Python 文件，开发者无需关注 HTTP 服务的实现，而专注于编写具体的业务逻辑。与通用服务不同，简单服务插件更加轻量化，通常适用于实现简单的业务操作。

### 简单服务特点

* 轻量级：只需一个 Python 文件，直接编写单个方法，快速实现功能。
* 无需 HTTP 实现：系统会自动处理 HTTP 接口和请求，不需要开发者手动配置。
* 快速集成：快速集成到插件系统中，可以立即作为一个后端服务进行使用。
* 简化业务逻辑：开发者只需关注核心的业务逻辑实现，而不需要处理与 HTTP 相关的部分。

## 创建简单服务插件包

在此处的示范中，我们将创建一个简单服务类型的插件。该插件的功能是对外提供一个加法运算接口。

:::tip
下文中的 MathService 就是我们即将创建的简单服务的插件名。
:::

### 步骤一：创建插件文件夹

首先我们需要创建一份插件基本文件夹，该文件夹需包含一个config.json配置文件和一个Python文件，注意简单服务中，**Python文件的名称必须与插件名称相同**。

您可以从头开始手动创建，也可以使用插件开发包仓库中 ["demo"](https://github.com/sh-agilebot/extension-toolkit/tree/master/demo/MathService) 目录下的模板进行修改。

目录结构:

```ultree
output: simple
MathService
  config.json
  MathService.py
```

```py [MathService.py]
# 获取全局logger实例，只能在简单服务中使用
logger = globals().get('logger')
if logger is None:
    # 本地调试时，使用自带日志库
    import logging
    logger = logging.getLogger(__name__)

def add(a: int, b: int) -> int:
    """
    执行两个整数的加法运算

    参数：
    - a (int): 第一个加数
    - b (int): 第二个加数

    返回：
    - int: 返回加法结果
    """
    try:
        result = a + b
        return result

    except Exception as ex:
        logger.error(ex)
        return 0
```

```json [config.json]
{
  "name": "MathService",
  "type": "easyService",
  "scriptLang": "python",
  "description": "数学服务",
  "version": "0.1"
}
```

### 步骤二：打包、安装

插件打包请参考[打包与安装](../04-package)

### 步骤三：调用接口

下面将介绍几种方式调用之前制作的接口。

* 方法1：使用`CALL_SERVICE`指令调用。

请参照[相关章节](../03-advanced/03-complex-backend#call-service)。

* 方法2：使用JS运行时在Web小程序中调用。

在Web小程序的 JS 代码中使用 `callEasyService` 函数调用。

```ts twoslash
import { callEasyService } from '@agilebot/extension-runtime';

callEasyService('MathService', 'add', {
  a: 1,
  b: 2
}).then(result => {
  // 输出：加法计算结果为 3
  console.log(`加法计算结果为${result}`);
});
```

具体示例可参考[复杂的Web小程序](../03-advanced/01-complex-page)

* 方法3：直接访问接口地址。

```
http://10.27.1.254:5616/MathService/add?a=1&b=2
```

在这种方式下，URL 查询参数（`a=1` 和 `b=2`）会被自动映射到 `MathService` 插件中的 `add` 函数的参数上：

* `a=1` 会被映射到函数 `add` 的 `a` 参数，值为 `1`。
* `b=2` 会被映射到函数 `add` 的 `b` 参数，值为 `2`。

以下是一个使用Python获取的例子：

```py
import requests

response = requests.get('http://10.27.1.254:5616/MathService/add', {
    'a': 1,
    'b': 2
})

if response.status_code == 200:
    # 解析 JSON 响应
    data = response.json()

    # 输出结果
    print(f"Result: {data['result']}")
else:
    print(f"Request failed with status code: {response.status_code}")
```

## 参数映射关系

| 函数参数类型 | 示例参数                          | 实际的URI地址                               | 参数映射说明                                                |
|--------------|-----------------------------------|---------------------------------------------|-------------------------------------------------------|
| `int`        | `a=1`                             | `?param1=1&param2=2`                        | `param1` 映射为函数的 `int` 类型参数，值为 `1`               |
| `str`        | `name=John`                       | `?name=John`                                | `name` 映射为函数的 `str` 类型参数，值为 `"John"`            |
| `bool`       | `isActive=true`                   | `?isActive=true`                            | `isActive` 映射为函数的 `bool` 类型参数，值为 `true`         |
| `List[dict]` | `items=[{"id":1,"name":"item1"}]` | `?items[0][id]=1&items[0][name]=item1` [^1] | `items` 映射为函数的 `List[dict]` 类型参数，值为一个字典列表 |

[^1]: 在JavaScript中可以使用[qs]\(https://www.npmjs.com/package/qs\)包序列化为这种格式。

## 局限性

虽然简单服务非常方便，但它的功能也有一些限制。以下是使用简单服务时需要注意的几个局限性：

1. 仅支持基本类型参数：简单服务的函数参数只支持以下基本类型：`str`、`int`、`bool`、`List[dict]`。如果需要处理更复杂的数据结构或自定义类型，建议使用通用服务来实现。
2. 扩展性受限：简单服务适用于快速开发和集成简单的业务逻辑。若涉及到高并发、复杂路由、状态管理等需求，通用服务会提供更高的灵活性和可扩展性。
3. 功能集中在业务逻辑上：简单服务专注于核心业务逻辑，而不涉及 HTTP 处理、请求验证、安全性等功能。如果您需要更复杂的请求处理（如认证、权限管理等），通用服务可以提供更多的功能支持。
