---
url: /02-development\03-advanced/03-complex-backend.md
---
# 简单服务中调用SDK

> 本页面旨在指导开发者如何在简单服务中调用Agilebot SDK，并通过程序指令调用。

## 创建简单服务插件包

在此处的示范中，我们将创建一个简单服务类型的插件。该插件的功能是对外提供一个加法运算接口，并写入某个R寄存器。

:::tip
下文中的 MathServiceComplex 就是我们即将创建的简单服务的插件名。
:::

### 步骤一：创建插件文件夹

首先我们需要创建一份插件基本文件夹，该文件夹需包含一个config.json配置文件和一个Python文件，注意简单服务中，**Python文件的名称必须与插件名称相同**。

您可以从头开始手动创建，也可以使用插件开发包仓库中 ["demo"](https://github.com/sh-agilebot/extension-toolkit/tree/master/demo/MathServiceComplex) 目录下的模板进行修改。

目录结构:

```ultree
output: simple
MathServiceComplex
  config.json
  MathServiceComplex.py
```

```py [MathServiceComplex.py]
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import Register

# 获取全局logger实例，只能在简单服务中使用
logger = globals().get('logger')
if logger is None:
    # 本地调试时，使用自带日志库
    import logging
    logger = logging.getLogger(__name__)


arm = Arm(dev_mode=True)
ret = arm.connect("10.27.1.254")
if ret != StatusCodeEnum.OK:
    logger.error("连接失败")


def add(a: int, b: int) -> int:
    """
    执行两个整数的加法运算，并写入寄存器

    参数：
    - a (int): 第一个加数
    - b (int): 第二个加数

    返回：
    - int: 返回加法结果
    """
    try:
        result = a + b
        # 将结果写入寄存器
        register = Register()
        register.id = 1
        register.name = "math_result"
        register.comment = "加法服务的结果"
        register.value = result

        ret = arm.register.write(1, register)
        if ret != StatusCodeEnum.OK:
            logger.error("更新R失败")


        return result

    except Exception as ex:
        logger.error(ex)
        return 0

```

```json [config.json]
{
  "name": "MathServiceComplex",
  "type": "easyService",
  "scriptLang": "python",
  "description": "数学服务",
  "version": "0.1"
}
```

### 步骤二：打包、安装

插件打包请参考[打包与安装](/02-development/04-package)

### 步骤三：使用`CALL_SERVICE`指令调用 {#call-service}

1. 选择插入指令`CALL_SERVICE`

![](./images/CallService1.png)

2. 填写`CALL_SERVICE`指令的相关参数

![](./images/CallService2.png)

* 服务名称：即简单服务的名称，本例中填写`MathServiceComplex`
* 指令名称：即要调用的服务中的函数名，本例中填写`add`
* 参数：即要传给上述函数名的参数列表，本例中填写`a: 1`、`b: 2`

3. 点击执行按钮

![](./images/CallService3.png)

4. 用户程序执行成功后，将在`R[1]`中写入值`3`

![](./images/CallService4.png)
