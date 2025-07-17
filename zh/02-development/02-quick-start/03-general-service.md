---
url: /zh/02-development/02-quick-start/03-general-service.md
---
# 通用服务开发

> 该页面旨在指导开发者如何开发通用服务类型的插件包。

## 关于通用服务

通用服务插件是用于实现复杂后端功能的插件。

与简单服务不同，通用服务插件需要开发者关注服务的配置、接口设计、请求处理、数据存储等内容，因此开发过程较为复杂，但也提供了更多的灵活性和扩展性。

### 通用服务特点

* 功能强大：可以处理更复杂的业务逻辑和数据操作。
* 灵活可扩展：可以根据业务需求扩展或修改服务的功能。
* 支持外部交互：能够与数据库、外部API或其他系统进行交互。
* 需要手动配置：相比简单服务，开发者需要配置 HTTP 接口、请求处理、路由等内容。

## 创建通用服务插件包

在此处的示范中，我们将创建一个通用服务类型的插件。该插件的功能是对外提供一个天气查询接口。

:::tip 提示
下文中的 WeatherService 就是我们即将创建的通用服务的插件名。
:::

### 步骤一：创建插件文件夹

首先我们需要创建一份插件基本文件夹，该文件夹需包含一个config.json配置文件和一个Python文件。

您可以从头开始手动创建，也可以使用插件开发包仓库中 ["demo"](https://github.com/sh-agilebot/extension-toolkit/tree/master/demo/WeatherService) 目录下的模板进行修改。

目录结构:

```ultree
output: simple
WeatherService
  config.json
  app.py
```

```py [app.py]
import os
import logging

from fastapi import FastAPI, HTTPException
from fastapi.middleware.cors import CORSMiddleware
import requests

# 动态获取端口号，普通服务的端口为自动分配
PORT = os.getenv("PORT", 8000)


logger = logging.getLogger(__name__)
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(filename)s:%(lineno)d - %(levelname)s - %(message)s',
)

app = FastAPI()
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"]
)

@app.get("/weather")
async def get_weather():
    """
    获取指定城市的天气
    :return: 城市天气信息
    """
    # 构建查询 URL
    url = f'http://t.weather.sojson.com/api/weather/city/101030100'
    try:
        response = requests.get(url)

        if response.status_code != 200:
            raise HTTPException(status_code=response.status_code, detail="请求天气数据失败")

        # 返回的数据是字符串，直接返回给客户端
        weather_info = response.json()

        return {"weather": weather_info}

    except requests.exceptions.RequestException as e:
        raise HTTPException(status_code=500, detail="请求外部天气服务失败")

if __name__ == "__main__":
    import uvicorn

    uvicorn.run(app, host="0.0.0.0", port=int(PORT))

```

```json [config.json]
{
  "name": "WeatherService",
  "type": "generalService",
  "scriptLang": "python",
  "description": "天气服务",
  "version": "0.1",
  "entry": "app.py"
}
```

### 步骤二：打包、安装

插件打包请参考[打包与安装](../04-package)

### 步骤三：调用接口

1. 与简单服务相同，通用服务需激活才能使用

![](/images/development/通用服务启动1.png)

2. 激活后，将看到服务端口号：

![](/images/development/通用服务启动2.png)

:::tip 提示
通用服务一经启动，重启时会优先被分配上次启动占据的端口号（若此时此端口号已被占用则会随机分配一个新的端口号）。
:::

3. 在其它程序中调用此接口：

```
http://10.27.1.254:6100/weather
```
