---
url: /1-python/4-methods.md
---

[#2]: ../2-glossary/

[#3.1]: ../3-struct/#3.1

[#3.2]: ../3-struct/#3.2

[#3.3]: ../3-struct/#3.3

[#3.4]: ../3-struct/#3.4

[#3.5]: ../3-struct/#3.5

[#3.6]: ../3-struct/#3.6

[#3.7]: ../3-struct/#3.7

[#3.8]: ../3-struct/#3.8

[#3.9]: ../3-struct/#3.9

[#3.10]: ../3-struct/#3.10

[#3.11]: ../3-struct/#3.11

[#3.12]: ../3-struct/#3.12

[#3.13]: ../3-struct/#3.13

[#3.14]: ../3-struct/#3.14

[#3.15]: ../3-struct/#3.15

[#3.16]: ../3-struct/#3.16

[#3.17]: ../3-struct/#3.17

[#3.18]: ../3-struct/#3.18

[#3.19]: ../3-struct/#3.19

[#3.20]: ../3-struct/#3.20

[#3.21]: ../3-struct/#3.21

[#3.22]: ../3-struct/#3.22

[#3.23]: ../3-struct/#3.23

[#3.24]: ../3-struct/#3.24

[#3.25]: ../3-struct/#3.25

[#3.26]: ../3-struct/#3.26

[#3.27]: ../3-struct/#3.27

[#3.28]: ../3-struct/#3.28

[#3.29]: ../3-struct/#3.29

[#3.30]: ../3-struct/#3.30

[#3.31]: ../3-struct/#3.31

[#3.32]: ../3-struct/#3.32

# 4 方法与示例

## 4.1 系统基础操作

### 4.1.1 连接机器人

| 方法名  | **connect** (`arm_controller_ip`: str) -> StatusCodeEnum                     |
|------|-----------------------------------------------------|
| 描述   | 根据控制柜IP连接机械臂                                        |
| 请求参数 | `arm_controller_ip`: str 控制柜IP地址 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                    |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")

# 打印结果
print(f"执行结果：{ret.errmsg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.2 判断与机械臂的连接是否有效

| 方法名  | **is\_connect**() -> bool                  |
|------|-----------------------------------|
| 描述   | 判断与机械臂的连接是否有效                     |
| 请求参数 | 无参数                               |
| 返回值  | bool: 连接状态，True: 连接有效，False: 连接失效 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 检查连接状态
connect_status = arm.is_connect()
# 打印结果
print(f"连接状态：{connect_status}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.3 与机器人断开连接

| 方法名  | **disconnect**() |
|------|------------------|
| 描述   | 断开和机器人的连接        |
| 请求参数 | 无参数              |
| 返回值  | 无返回              |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")

# 打印结果
print(f"执行结果：{ret.errmsg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.4 获取当前机器人型号

| 方法名  | **get\_arm\_model\_info**() -> tuple\[str, StatusCodeEnum]           |
|------|-----------------------------------------------------------|
| 描述   | 获取当前机器人型号信息                                               |
| 请求参数 | 无参数                                                       |
| 返回值  |str: 机器人型号如"GBT-P7A-700"   [StatusCodeEnum][#3.1]: 函数执行结果 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取型号
model_info, ret = arm.get_arm_model_info()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"机器人型号：{model_info}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.5 获取机器人运行状态

| 方法名  | **get\_robot\_status**() -> tuple\[RobotStatusEnum, StatusCodeEnum]       |
|------|-----------------------------------------------------------------|
| 描述   | 获取机器人运行状态                                                       |
| 请求参数 | 无参数                                                             |
| 返回值  | [RobotStatusEnum][#3.2]: 机器人运行状态   [StatusCodeEnum][#3.1]: 函数执行结果 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取机器人运行状态
ret, state = arm.get_robot_status()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"机器人运行状态：{state.msg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.6 获取当前控制器运行状态

| 方法名  | **get\_ctrl\_status**() -> tuple\[CtrlStatusEnum, StatusCodeEnum]           |
|------|--------------------------------------------------------------|
| 描述   | 获取当前控制器运行状态                                                  |
| 请求参数 | 无参数                                                          |
| 返回值  | [CtrlStatusEnum][#3.3]: 控制器运行状态  [StatusCodeEnum][#3.1]: 函数执行结果    |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取控制器运行状态
ret, state = arm.get_ctrl_status()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"控制器运行状态：{state.msg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.7 获取当前伺服控制器状态

| 方法名  | **get\_servo\_status**() -> tuple\[ServoStatusEnum, StatusCodeEnum]  |
|------|-----------------------------------------------------------------|
| 描述   | 获取当前伺服控制器状态                   |
| 请求参数 | 无参数                                                |
| 返回值  | [ServoStatusEnum][#3.4]: 伺服控制器状态    [StatusCodeEnum][#3.1]: 函数执行结果 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取伺服控制器状态
ret, state = arm.get_servo_status()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"伺服控制器状态：{state.msg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.8 获取机器人当前的软状态

| 方法名  | **get\_soft\_mode**() -> tuple\[SoftModeEnum, StatusCodeEnum]      |
|------|--------------------------------------------------------------|
| 描述   | 获取机器人当前的软状态                                    |
| 请求参数 | 无参数                                                |
| 返回值  | [SoftModeEnum][#3.5]: 伺服控制器状态   [StatusCodeEnum][#3.1]: 函数执行结果|

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取机器人当前的软状态
state, ret = arm.get_soft_mode()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"机器人当前的软状态：{state.name}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.9 设置机器人当前的软状态

| 方法名  | **set\_soft\_mode**(`soft_mode`: SoftModeEnum) -> StatusCodeEnum|
|------|--------------------------------------|
| 描述   | 设置机器人当前的软状态 (PC模式下的手/自动状态)           |
| 请求参数 | `soft_mode`: [SoftModeEnum][#3.5] 软状态值           |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import SoftModeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置机器人当前的软状态为手动限速模式
ret = arm.set_soft_mode(SoftModeEnum.MANUAL_LIMIT)
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"机器人软状态设定结果：{ret.errmsg}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.10 上位机获取操作权限

| 方法名  | **acquire\_access**()         |
|------|------------------------------|
| 描述   | 上位机获取操作权限，使机器人进入[PC模式][#2] |
| 请求参数 | 无参数                          |
| 返回值  | 无返回                          |
| 备注   | 仅适用于SCARA机器人，P7A及协作无需使用     |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取权限
arm.acquire_access()

# 返还权限
arm.release_access()

# 结束后断开机器人连接
arm.disconnect()
```

### 4.1.11 上位机返还操作权限

| 方法名  | **release\_access**()         |
|------|------------------------------|
| 描述   | 上位机返还操作权限，使机器人退出[PC模式][#2] |
| 请求参数 | 无参数                          |
| 返回值  | 无返回                          |
| 备注   | 仅适用于SCARA机器人，P7A及协作无需使用        |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取权限
arm.acquire_access()

# 返还权限
arm.release_access()

# 结束后断开机器人连接
arm.disconnect()
```

### 4.1.12 获取控制器版本

| 方法名  | **get\_version**() -> tuple\[str, StatusCodeEnum]      |
|------|----------------------------------------------|
| 描述   | 获取控制器版本                                      |
| 请求参数 | 无参数                                          |
| 返回值  | str: 控制器版本   [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取控制器版本
version_info, ret = arm.get_version()
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"控制器版本：{version_info}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.13 开关机器人本体LED灯光

| 方法名  | **switch\_led\_light**(`mode`: bool) -> StatusCodeEnum        |
|------|----------------------------------------------|
| 描述   | 开关机器人本体LED灯光                                      |
| 请求参数 | `mode`: bool，True为打开，False为关闭          |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果    |
| 兼容性   | 协作机器人控制器版本 1.3.6 及以上版本支持，工业机器人不支持         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 控制LED灯光
ret = arm.switch_led_light(mode = False)
# 检查是否成功
assert ret == StatusCodeEnum.OK
# 打印结果
print(f"操作完成")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.1.14 机器人伺服上电

| 方法名  | **servo\_on**() -> StatusCodeEnum |
|------|--------------------------|
| 描述   | 让机械臂伺服上电                 |
| 请求参数 | 无参数                      |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果    |

### 4.1.15 机器人伺服下电

| 方法名  | **servo\_off**() -> StatusCodeEnum |
|------|---------------------------|
| 描述   | 让机器人伺服下电                  |
| 请求参数 | 无参数                       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |

### 4.1.16 机器人伺服重置

| 方法名  | **servo\_reset**() -> StatusCodeEnum |
|------|---------------------------|
| 描述   | 让机器人伺服重置                  |
| 请求参数 | 无参数                       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
import time

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 机器人伺服重置
ret = arm.servo_reset()
assert ret == StatusCodeEnum.OK
time.sleep(5)

# 机器人伺服下电
ret = arm.servo_off()
assert ret == StatusCodeEnum.OK
time.sleep(5)

# 机器人伺服上电
ret = arm.servo_on()
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.2 机器人运动控制和状态

### 4.2.1 获取机器人参数

#### 4.2.1.1 获取 OVC 全局速度比率

| 方法名  | **motion.get\_OVC**() -> tuple\[float, StatusCodeEnum]|
|------|-----------------------------------------|
| 描述   | 获取当前机器人 OVC 全局速度比率           |
| 请求参数 | 无参数               |
| 返回值  | float：速度比率, 结果在0~1之间  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.2.1.2 获取 OAC 全局加速度比率

| 方法名  | **motion.get\_OAC**() -> tuple\[float, StatusCodeEnum]|
|------|-----------------------------------------|
| 描述   | 获取当前机器人 OAC 全局加速度比率           |
| 请求参数 | 无参数               |
| 返回值  | float：速度比率, 结果在0~1.2之间  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.2.1.3 获取当前使用的 TF 用户坐标系编号

| 方法名  | **motion.get\_TF**() -> tuple\[int, StatusCodeEnum]|
|------|-----------------------------------------|
| 描述   | 获取当前机器人使用的 TF 用户坐标系编号          |
| 请求参数 | 无参数               |
| 返回值  | int: 用户坐标系编号  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.2.1.4 获取当前使用的 UF 工具坐标系编号

| 方法名  | **motion.get\_UF**() -> tuple\[int, StatusCodeEnum]|
|------|-----------------------------------------|
| 描述   | 获取当前机器人使用的 UF 工具坐标系编号          |
| 请求参数 | 无参数               |
| 返回值  | int: 工具坐标系编号  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.2.1.5 获取当前使用的 TCS 示教坐标系

| 方法名  | **motion.get\_TCS**() -> tuple\[TCSType, StatusCodeEnum]|
|------|-----------------------------------------|
| 描述   | 获取当前机器人使用的 TCS 示教坐标系          |
| 请求参数 | 无参数               |
| 返回值  | [TCSType][#3.7]: 示教坐标系编号  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import TCSType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置机器人各参数
ret = arm.motion.set_OVC(0.7)
assert ret == StatusCodeEnum.OK

ret = arm.motion.set_OAC(0.7)
assert ret == StatusCodeEnum.OK

ret = arm.motion.set_TCS(TCSType.TOOL)
assert ret == StatusCodeEnum.OK

ret = arm.motion.set_UF(0)
assert ret == StatusCodeEnum.OK

ret = arm.motion.set_TF(0)
assert ret == StatusCodeEnum.OK

print(f"参数设置成功")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.2 设置机器人参数

#### 4.2.2.1 设置 OVC 全局速度比率

| 方法名  | **motion.set\_OVC**(`value`: float) -> StatusCodeEnum  |
|------|---------------------------------------|
| 描述   | 设置机器人的 OVC 全局速度比率            |
| 请求参数 | `value`: float，速度比率范围是0~1        |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

#### 4.2.2.2 设置 OAC 全局加速度比率

| 方法名  | **motion.set\_OAC**(`value`: float) -> StatusCodeEnum  |
|------|---------------------------------------|
| 描述   | 设置机器人的 OAC 全局加速度比率            |
| 请求参数 | `value`: float，加速度比率, 0~1.2之间       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

#### 4.2.2.3 设置当前使用的 TF 用户坐标系

| 方法名  | **motion.set\_TF**(`value`: int) -> StatusCodeEnum  |
|------|---------------------------------------|
| 描述   | 设置机器人当前使用的 TF 用户坐标系            |
| 请求参数 | `value`: int, 用户坐标系编号       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

#### 4.2.2.4 设置当前使用的 UF 工具坐标系

| 方法名  | **motion.set\_UF**(`value`: int) -> StatusCodeEnum  |
|------|---------------------------------------|
| 描述   | 设置机器人当前使用的 UF 工具坐标系            |
| 请求参数 | `value`: int, 工具坐标系编号       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

#### 4.2.2.5 设置当前使用的 TCS 示教坐标系

| 方法名  | **motion.set\_TCS**(`value`: TCSType) -> StatusCodeEnum  |
|------|---------------------------------------|
| 描述   | 设置机器人当前使用的 TCS 示教坐标系            |
| 请求参数 | `value`: [TCSType][#3.7], 示教坐标系       |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import TCSType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取机器人各参数并打印
res, ret = arm.motion.get_OVC()
assert ret == StatusCodeEnum.OK
print(f"全局速度比率：{res}")

res, ret = arm.motion.get_OAC()
assert ret == StatusCodeEnum.OK
print(f"全局加速度比率：{res}")

res, ret = arm.motion.get_TCS()
assert ret == StatusCodeEnum.OK
print(f"示教坐标系类型：{TCSType(res).name}")

res, ret = arm.motion.get_UF()
assert ret == StatusCodeEnum.OK
print(f"用户坐标系：{res}")

res, ret = arm.motion.get_TF()
assert ret == StatusCodeEnum.OK
print(f"工具坐标系：{res}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.3 将笛卡尔点位转换成关节值点位

| 方法名  |  **motion.convert\_cart\_to\_joint**(`pose`: MotionPose, `uf_index`: int = 0, `tf_index`: int = 0) -> tuple\[MotionPose, StatusCodeEnum]    |
|------|----------------------------------------------------------------------------|
| 描述   | 将笛卡尔点位转换成关节值点位     |
| 请求参数 | `pose`: [MotionPose][#3.7] 机器人的关节位姿   `uf_index`: int 用户坐标系id  `tf_index`: int 工具坐标系id|
| 返回值  |[MotionPose][#3.7]: 机器人点位  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.2.4 将关节值点位转换成笛卡尔点位

| 方法名  |  **motion.convert\_joint\_to\_cart**(`pose`: MotionPose, `uf_index`: int = 0, `tf_index`: int = 0) -> tuple\[MotionPose, StatusCodeEnum]    |
|------|----------------------------------------------------------------------------|
| 描述   | 将关节值点位转换成笛卡尔点位     |
| 请求参数 | `pose`: [MotionPose][#3.7] 机器人的关节位姿   `uf_index`: int 用户坐标系id  `tf_index`: int 工具坐标系id|
| 返回值  |[MotionPose][#3.7]: 机器人点位  [StatusCodeEnum][#3.1]: 函数执行结果 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import MotionPose
from Agilebot.IR.A.sdk_types import PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 初始化位姿
motion_pose = MotionPose()
motion_pose.pt = PoseType.CART
motion_pose.cartData.position.x = 221.5
motion_pose.cartData.position.y = -494.1
motion_pose.cartData.position.z = 752.0
motion_pose.cartData.position.a = -89.1
motion_pose.cartData.position.b = 31.6
motion_pose.cartData.position.c = -149.3

# 转换关节值坐标
joint_pose, ret = arm.motion.convert_cart_to_joint(motion_pose)
assert ret == StatusCodeEnum.OK

# 打印结果位姿
print(f"位姿类型：{joint_pose.pt}")
print(
    f"轴位置：\n"
    f"J1:{joint_pose.joint.j1}\n"
    f"J2:{joint_pose.joint.j2}\n"
    f"J3:{joint_pose.joint.j3}\n"
    f"J4:{joint_pose.joint.j4}\n"
    f"J5:{joint_pose.joint.j5}\n"
    f"J6:{joint_pose.joint.j6}"
)

# 转换笛卡尔坐标
cart_pose, ret = arm.motion.convert_joint_to_cart(joint_pose)
assert ret == StatusCodeEnum.OK

# 打印结果位姿
print(f"位姿类型：{cart_pose.pt}")
print(
    f"笛卡尔位置：\n"
    f"X:{cart_pose.cartData.position.x}\n"
    f"Y:{cart_pose.cartData.position.y}\n"
    f"Z:{cart_pose.cartData.position.z}"
)

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.5 让机器人末端移动到指定的位置

| 方法名  | **motion.move\_joint**(`pose`: MotionPose, `vel`: float = 1, `acc`: float = 1)  -> StatusCodeEnum     |
|------|------------------------------|
| 描述   | 让机器人末端移动到指定的位置  |
| 请求参数 | `pose`: [MotionPose][#3.7] 笛卡尔空间或关节坐标系上的一个点的坐标   `vel`: float 运动的速度，范围是0~1, 表示最大速度的倍数  `acc`: float 范围是0~1.2, 表示最大加速度的倍数   |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import MotionPose
from Agilebot.IR.A.sdk_types import PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 初始化位姿
motion_pose = MotionPose()
motion_pose.pt = PoseType.JOINT
motion_pose.joint.j1 = 0
motion_pose.joint.j2 = 0
motion_pose.joint.j3 = 60
motion_pose.joint.j4 = 60
motion_pose.joint.j5 = 0
motion_pose.joint.j6 = 0

# 发送运动请求
ret = arm.motion.move_joint(motion_pose, vel = 0.5, acc = 0.5)
assert ret == StatusCodeEnum.OK

print(f"运动成功")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.6 让机器人末端沿直线移动到指定的位置

| 方法名  | **motion.move\_line**(`pose`: MotionPose, `vel`: float = 100, `acc`: float = 1)  -> StatusCodeEnum     |
|------|------------------------------|
| 描述   | 让机器人末端沿直线移动到指定的位置  |
| 请求参数 | `pose`: [MotionPose][#3.7] 笛卡尔空间或关节坐标系上的一个点的坐标   `vel`: float 运动的速度，范围是0~5000mm/s, 表示机械臂末端移动速度  `acc`: float 范围是0~1.2, 表示最大加速度的倍数   |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import MotionPose
from Agilebot.IR.A.sdk_types import PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 初始化位姿
motion_pose = MotionPose()
motion_pose.pt = PoseType.JOINT
motion_pose.joint.j1 = 0
motion_pose.joint.j2 = 0
motion_pose.joint.j3 = 60
motion_pose.joint.j4 = 60
motion_pose.joint.j5 = 0
motion_pose.joint.j6 = 0

# 发送运动请求
ret = arm.motion.move_line(motion_pose, vel = 100, acc = 0.5)
assert ret == StatusCodeEnum.OK

print(f"运动成功")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.7 让机器人末端沿弧线移动到指定的位置

| 方法名  | **motion.move\_circle**(`pose1`: MotionPose, `pose2`: MotionPose, `vel`: float = 100, `acc`: float = 1.0)  -> StatusCodeEnum     |
|------|------------------------------|
| 描述   | 让机器人末端沿弧线移动到指定的位置  |
| 请求参数 | `pose1`: [MotionPose][#3.7] 机械臂运动的途径点位姿  `pose2`: [MotionPose][#3.7] 机械臂运动的终点位姿   `vel`: float 运动的速度，范围是0~5000mm/s, 表示机械臂末端移动速度  `acc`: float 范围是0~1.2, 表示最大加速度的倍数   |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from multiprocessing.connection import wait
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import MotionPose
from Agilebot.IR.A.sdk_types import PoseType
import time

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 初始化位姿
motion_pose = MotionPose()
motion_pose.pt = PoseType.CART
motion_pose.cartData.position.x = 377.000
motion_pose.cartData.position.y = 202.820
motion_pose.cartData.position.z = 507.155
motion_pose.cartData.position.c = 0
motion_pose.cartData.position.b = 0
motion_pose.cartData.position.a = 0

# 运动到初始点
ret = arm.motion.move_joint(motion_pose)
assert ret == StatusCodeEnum.OK

# 修改为运动中间点
motion_pose.cartData.position.x = 488.300
motion_pose.cartData.position.y = 359.120
motion_pose.cartData.position.z = 507.155

# 运动终点
motion_pose2 = MotionPose()
motion_pose2.pt = PoseType.CART
motion_pose2.cartData.position.x = 629.600
motion_pose2.cartData.position.y = 509.270
motion_pose2.cartData.position.z = 507.155
motion_pose2.cartData.position.c = 0
motion_pose2.cartData.position.b = 0
motion_pose2.cartData.position.a = 0

# 等待运动结束
time.sleep(5)

# 开始运动
ret_code = arm.motion.move_circle(motion_pose, motion_pose2, vel = 100)
assert ret_code == StatusCodeEnum.OK
print(f"运动成功")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.8 获取机器人的当前位姿

| 方法名  | **motion.get\_current\_pose**(`pose_type`: PoseType, `uf_index`: int = 0, `tf_index`: int = 0) -> tuple\[MotionPose, StatusCodeEnum]       |
|------|-------------------------------------------------------------------|
| 描述   | 获取机器人的当前位姿                              |
| 请求参数 | `pose_type`:[PoseType][#3.6] 位姿类型   `uf_index`: 当使用PoseType.CART时需传入用户坐标系id, 默认0  `tf_index` : 当使用PoseType.CART时需传入工具坐标系id, 默认0 |
| 返回值  | [MotionPose][#3.7]: 机器人点位  [StatusCodeEnum][#3.1]: 函数执行结果      |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取当前位姿
motion_pose, ret = arm.motion.get_current_pose(PoseType.JOINT)
assert ret == StatusCodeEnum.OK

# 打印结果位姿
print(f"位姿类型：{motion_pose.pt}")
print(
    f"轴位置：\n"
    f"J1:{motion_pose.joint.j1}\n"
    f"J2:{motion_pose.joint.j2}\n"
    f"J3:{motion_pose.joint.j3}\n"
    f"J4:{motion_pose.joint.j4}\n"
    f"J5:{motion_pose.joint.j5}\n"
    f"J6:{motion_pose.joint.j6}"
)

# 获取当前位姿
motion_pose, ret = arm.motion.get_current_pose(PoseType.CART, 0, 0)
assert ret == StatusCodeEnum.OK

# 打印结果位姿
print(f"位姿类型：{motion_pose.pt}")
print(
    f"坐标位置：\n"
    f"X:{motion_pose.cartData.position.x}\n"
    f"Y:{motion_pose.cartData.position.y}\n"
    f"Z:{motion_pose.cartData.position.z}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.9 获取机器人的DH参数

| 方法名  | **motion.get\_DH\_param**() -> tuple\[list\[DHparam], StatusCodeEnum] |
|------|------------------------------------------------------|
| 描述   | 获取机器人的DH参数 结构见DHparam                                |
| 请求参数 | 无参数                                                  |
| 返回值  | list([DHparam][#3.8]): DH参数列表  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取DH参数
res, ret = arm.motion.get_DH_param()
assert ret == StatusCodeEnum.OK

# 打印结果
for param in res:
    print(
        f"DH参数的ID:{param.id}\n"
        f"杆件长度:{param.a}\n"
        f"杆件扭角:{param.alpha}\n"
        f"关节距离:{param.d}\n"
        f"关节转角:{param.offset}"
    )

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.10 设置机器人的DH参数

| 方法名  | **motion.set\_DH\_param**(`dh_list`: list\[DHparam]) -> StatusCodeEnum |
|------|----------------------------------|
| 描述   | 设置机器人的DH参数                       |
| 请求参数 | `dh_list`： list([DHparam][#3.8]) DH参数列表           |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取DH参数
res, ret = arm.motion.get_DH_param()
assert ret == StatusCodeEnum.OK

# 修改DH参数
res[0].a = 100
res[0].alpha = 0
res[0].d = 366
res[0].offset = 0

# 设置DH参数
ret = arm.motion.set_DH_param(res)
assert ret == StatusCodeEnum.OK

# 打印结果
for param in res:
    print(
        f"DH参数的ID:{param.id}\n"
        f"杆件长度:{param.a}\n"
        f"杆件扭角:{param.alpha}\n"
        f"关节距离:{param.d}\n"
        f"关节转角:{param.offset}"
    )

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.11 获取机器人轴锁定状态

| 方法名  | **motion.get\_drag\_set**() -> tuple\[DragStatus, StatusCodeEnum]               |
|------|------------------------------------------------|
| 描述   | 获取当前机器人轴锁定状态                     |
| 请求参数 | 无参数                                 |
| 返回值  | [DragStatus][#3.15]: 轴锁定状态, Ture表示该轴为可移动状态，False表示被锁定 [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取当前轴锁定状态
drag_status, ret = arm.motion.get_drag_set()
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"当前X轴拖动状态：{drag_status.cart_status.x}\n"
    f"当前Y轴拖动状态：{drag_status.cart_status.y}\n"
    f"当前Z轴拖动状态：{drag_status.cart_status.z}"
)

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.12 设定机器人轴锁定状态

| 方法名  | **motion.set\_drag\_set**(`drag_status`: DragStatus) -> StatusCodeEnum  |
|------|-------------------------------------------------------|
| 描述   | 设定当前机器人轴锁定状态                                          |
| 请求参数 | `drag_status`：[DragStatus][#3.15] 各轴的锁定状态，默认全部为Ture: 解锁状态 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                                 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import DragStatus
from Agilebot.IR.A.sdk_types import TCSType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置示教坐标系
arm.motion.set_TCS(TCSType.BASE)
assert ret == StatusCodeEnum.OK

# 设置要锁定的轴
drag_status = DragStatus()
drag_status.cart_status.x = False
drag_status.cart_status.y = False
# 设置连续拖动开关
drag_status.is_continuous_drag = True

# 设置轴锁定状态
ret = arm.motion.set_drag_set(drag_status)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"当前X轴拖动状态：{drag_status.cart_status.x}\n"
    f"当前Y轴拖动状态：{drag_status.cart_status.y}\n"
    f"当前Z轴拖动状态：{drag_status.cart_status.z}"
    )

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.13 设定当前机器人是否启动拖动

| 方法名  | **motion.enable\_drag**(`drag_state`: bool) -> StatusCodeEnum |
|------|------------------------------------------------|
| 描述   | 设定当前机器人是否启动拖动                                   |
| 请求参数 | `drag_state`：bool 机器人是否允许拖动，True表示进入拖动状态，False表示退出拖动状态 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                          |
| 兼容性   | 协作机器人控制器版本 1.3.2 及以上版本，工业机器人 1.2.1 及以上版本 支持        |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 进入拖动示教
ret = arm.motion.enable_drag(True)
assert ret == StatusCodeEnum.OK

# 打印结果
print("开始拖动示教")

# 退出拖动示教
ret = arm.motion.enable_drag(False)
assert ret == StatusCodeEnum.OK

# 打印结果
print("退出拖动示教")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.2.14 进入实时位置控制模式

| 方法名  | **motion.enter\_position\_control**() -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 进入实时位置控制模式，允许对机器人进行精确的位置控制 |
| 请求参数 | 无 |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果 |
| 备注     | 在进入实时控制模式后，必须通过UDP发送控制指令 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

### 4.2.15 退出实时位置控制模式

| 方法名  | **motion.exit\_position\_control**() -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 退出实时位置控制模式，恢复默认的机器人控制状态 |
| 请求参数 | 无 |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果 |
| 备注   | 退出后，机器人将不再接受实时控制指令 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

### 4.2.16 设置udp反馈参数

| 方法名  | **motion.set\_udp\_feedback\_params**(`flag`: bool, `ip`: str, `interval`: int, `feedback_type`: int, `DO_list`: list\[int] = None) -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 配置机器人向指定IP地址推送数据的udp反馈参数 |
| 请求参数 | `flag`：bool 是否开启UDP数据推送；`ip`：str 接收端的IP地址；`interval`：int 发送数据的间隔（单位：毫秒）；`feedbackType`：int 反馈数据格式（0：XML格式）；`DOList`：list\[int] 期望获取的DO信号列表（最多十个，可选） |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果                |
| 备注   | 参数设置仅在UDP数据推送功能启用时有效                     |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本支持，工业机器人不支持         |

#### 推送数据说明

| 名称 | 字段 | 描述 |
|------|------|------|
| **RIst: 笛卡尔位置** | X | 工具坐标系下 X 方向值，单位为毫米 |
| | Y | 工具坐标系下 Y 方向值，单位为毫米 |
| | Z | 工具坐标系下 Z 方向值，单位为毫米 |
| | A | 工具坐标系下绕 X 方向旋转，单位为度 |
| | B | 工具坐标系下绕 Y 方向旋转，单位为度 |
| | C | 工具坐标系下绕 Z 方向旋转，单位为度 |
| **AIPos: 关节位置** | A1-A6 | 六个关节的值，单位为角度 |
| **EIPos: 附加轴数据** | EIPos | 附加轴数据 |
| **WristBtnState: 手腕按键状态** | 按键状态 | 1 = 按键按下，0 = 按键抬起 |
| | DragModel | 拖拽按键状态|
| | RcordJoint | 示教记录按键状态 |
| | PauseResume | 暂停恢复按键状态 |
| **Digout: DO 输出** | Digout | 数字输出（DO）的状态 |
| **ProgramStatus: 程序状态** | ProgId | 程序 ID |
| | Status | 解释器执行状态：0 = INTERPRETER\_IDLE1 = INTERPRETER\_EXECUTE2 = INTERPRETER\_PAUSED |
| | Xpath | 程序片段返回值，格式为 `程序名:行号` |
| **IPOC: 时间戳** | IPOC | 时间戳 |

### 4.2.17 负载相关接口

#### 4.2.17.1 获取当前激活的负载编号

| 方法名  | **motion.payload.get\_current\_payload**() -> tuple\[int, StatusCodeEnum] |
|------|----------------------------------------|
| 描述   | 获取当前激活的负载编号，返回对应的ID编号                  |
| 请求参数 | 无参数                                    |
| 返回值  | int: 负载编号  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取当前激活负载
current_payload_id, ret = arm.motion.payload.get_current_payload()
assert ret == StatusCodeEnum.OK

# 打印结果
print(f"当前激活负载ID为：{current_payload_id}")

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.2 根据指定编号获取负载信息

| 方法名  | **motion.payload.get\_payload\_by\_id**(`payload_id`: int) -> tuple\[Payload, StatusCodeEnum]    |
|------|-----------------------------------------------------|
| 描述   | 获取指定编号的负载信息                                         |
| 请求参数 | `payload_id`: int 指定的负载ID编号                         |
| 返回值  | [Payload][#3.14]: 负载信息  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取负载
res, ret = arm.motion.payload.get_payload_by_id(1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"负载ID:{res.id}\n"
    f"负载质量:{res.m_load}\n"
    f"负载注释:{res.comment}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.3 根据指定编号激活负载

| 方法名  | **motion.payload.set\_current\_payload**(`payload_id`: int) -> StatusCodeEnum |
|------|--------------------------------------------|
| 描述   | 根据指定编号激活负载                                 |
| 请求参数 | `payload_id`: int 指定的负载ID编号                      |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                      |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 指定编号激活负载
ret = arm.motion.payload.set_current_payload(1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(f"当前激活负载ID为：1")

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.4 向机器人控制柜添加一个用户自定义负载信息

| 方法名  | **motion.payload.add\_payload**(`payload_info`: Payload) -> StatusCodeEnum |
|------|----------------------------------------------|
| 描述   | 向机器人控制柜添加一个用户自定义负载信息 |
| 请求参数 | `payload_info`: [Payload][#3.14] 用户自定义负载信息        |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果              |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.flyshot import Payload

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 初始化负载
new_payload = Payload()
new_payload.id = 6
new_payload.m_load = 18
new_payload.lcx_load = -151
new_payload.lcy_load = 1.0
new_payload.lcz_load = 75
new_payload.Ixx_load = 0.11
new_payload.Iyy_load = 0.61
new_payload.Izz_load = 0.54
new_payload.comment = 'Test'.encode('utf-8')

# 添加负载
ret = arm.motion.payload.add_payload(new_payload)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"负载ID:{new_payload.id}\n"
    f"负载质量:{new_payload.m_load}\n"
    f"负载注释:{new_payload.comment}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.5 根据指定编号删除对应的负载信息

| 方法名  | **motion.payload.delete\_payload**(`payload_id`: int) -> StatusCodeEnum     |
|------|-------------------------------------------|
| 描述   | 向控制器删除一个用户自定义负载                           |
| 请求参数 | `payload_id`: int 指定的负载ID编号                     |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                     |
| 备注   | 注意：无法删除当前激活的负载，如果要删除激活的负载，请先激活其他负载再删除当前负载 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 删除指定ID负载
ret = arm.motion.payload.delete_payload(6)
assert ret == StatusCodeEnum.OK

# 打印结果
print(f"删除负载6成功")

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.6 更新一个已存在负载信息

| 方法名  | **motion.payload.update\_payload**(`payload_info`: Payload) -> StatusCodeEnum       |
|------|-----------------------------------------------|
| 描述   | 向机器人更新一个已存在的用户自定义负载的信息                 |
| 请求参数 | `payload_info`: [Payload][#3.9] 用户自定义更新负载的信息   |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                    |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取负载
payload_info, ret_code = arm.motion.payload.get_payload_by_id(1)
payload_info.comment = 'Test'.encode('utf-8')

# 更新负载
ret = arm.motion.payload.update_payload(payload_info)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"负载ID:{payload_info.id}\n"
    f"负载质量:{payload_info.m_load}\n"
    f"负载注释:{payload_info.comment}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.7 获取所有负载信息

| 方法名  | **motion.payload.get\_all\_payload**() -> tuple\[list, StatusCodeEnum] |
| ---- | ---------------------------- |
| 描述   | 获取所有负载信息                |
| 请求参数 |  无参数                      |
| 返回值   | list : 所有负载信息列表 [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.common.const import const

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取所有负载
res, ret = arm.motion.payload.get_all_payload()
assert ret == StatusCodeEnum.OK

# 打印结果
for payload in res:
    print(
            f"负载ID:{payload[0]}\n"
            f"负载注释:{payload[1]}\n"
        )

# 结束后断开机器人连接
arm.disconnect()

```

#### 4.2.17.8 检测3轴是否水平

| 方法名  | **motion.payload.check\_axis\_three\_horizontal**() -> tuple\[float, StatusCodeEnum] |
| ---- | ---------------------------- |
| 描述   | 检测3轴是否水平 |
| 请求参数 | 无  |
| 返回值   | float: 返回3轴的水平角度, 单位为度  [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 水平的角度，必须在-1~1之间才能进行负载测定 |

#### 4.2.17.9 获取负载测定状态

| 方法名  | **motion.payload.get\_payload\_identify\_state**() -> tuple\[PayloadIdentifyState, StatusCodeEnum] |
| ---- | ---------------------------- |
| 描述   | 获取负载测定的状态 |
| 请求参数 | 无  |
| 返回值   | [PayloadIdentifyState][#3.31] 返回负载测定状态  [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 无 |

#### 4.2.17.10 开始负载测定

| 方法名  | **motion.payload.start\_payload\_identify**(`weight`: float, `angle`: float) -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 开始负载测定 |
| 请求参数 | `weight`：float 负载重量（未知重量填-1）； `angle`：float 6轴允许转动的角度（30-90度） |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 开始负载测定前必须先进入负载测定状态 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持    |

#### 4.2.17.11 获取负载测定结果

| 方法名  | **motion.payload.payload\_identify\_result**() -> tuple\[Payload, StatusCodeEnum] |
| ---- | ---------------------------- |
| 描述   | 获取负载测定的结果 |
| 请求参数 | 无  |
| 返回值   | [Payload][#3.6]: 返回负载测定结果[StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 无 |

#### 4.2.17.12 开始干涉检查

| 方法名  | **motion.payload.interference\_check\_for\_payload\_identify**(`weight`: float, `angle`: float) -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 开始负载测定的干涉检查 |
| 请求参数 | `weight`: float 负载重量；`angle`: float 6轴转动角度（30-90度） |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 无 |

#### 4.2.17.13 进入负载测定状态

| 方法名  | **motion.payload.payload\_identify\_start**() -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 进入负载测定状态 |
| 请求参数 | 无  |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 无 |

#### 4.2.17.14 结束负载测定状态

| 方法名  | **motion.payload.payload\_identify\_done**() -> StatusCodeEnum |
| ---- | ---------------------------- |
| 描述   | 结束负载测定状态 |
| 请求参数 | 无  |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 无 |

#### 4.2.17.15 负载测定全流程

| 方法名  | **motion.payload.payload\_identify**(`weight`: float, `angle`: float) -> tuple\[Payload, StatusCodeEnum] |
| ---- | ---------------------------- |
| 描述   | 完整的负载测定流程 |
| 请求参数 | `weight`: float 负载重量（未知重量填-1）；`angle`: float 6轴转动角度（30-90度）|
| 返回值   | [Payload][#3.6]: 负载测定结果  [StatusCodeEnum][#3.1]: 函数执行结果  |
| 备注   | 返回的负载可以新增到机器人中或写入机器人中已有的某个负载  全流程步骤： 1.移动到指定水平位并检测是否水平 2.进入负载测定状态 3.开始负载测定 4.获取负载测定结果 5.结束负载测定状态|
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本支持，工业机器人不支持         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

motion_pose = MotionPose()
motion_pose.pt = const.JOINT

motion_pose.joint.j1 = 0
motion_pose.joint.j2 = 0
motion_pose.joint.j3 = 0
motion_pose.joint.j4 = 0
motion_pose.joint.j5 = 0
motion_pose.joint.j6 = 0

# 运动到指定点
code = arm.motion.move_to_pose(motion_pose, const.MOVE_JOINT)
if code != StatusCodeEnum.OK:
    return None, code

while True:
    # 获取伺服状态
    code ,state= arm.get_servo_status()
    if code != StatusCodeEnum.OK:
        return None, code

    if state == ServoStatusEnum.SERVO_IDLE:
        break
    else:
        time.sleep(1)

# 开始负载测定并获取结果
res, ret =  arm.motion.payload.payload_identify(-1, 90)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.3 机器人程序操作类

### 4.3.1 执行某个指定的程序

| 方法名  | **execution.start**(`program_name`: str) -> StatusCodeEnum |
|------|-----------------------------------|
| 描述   | 执行某个指定的程序                         |
| 请求参数 | `program_name`: str 需要执行的程序名称           |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果             |

### 4.3.2 停止某个程序执行

| 方法名  | **execution.stop**(`program_name`: str = '') -> StatusCodeEnum |
|------|----------------------------------|
| 描述   | 停止某个程序执行                         |
| 请求参数 | `program_name`: str 需要停止的程序名称, 默认为空字符串，表示停止当前正在运行的程序或运动指令|
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 执行程序 
ret = arm.execution.start(program_name)
assert ret == StatusCodeEnum.OK

# 停止程序
ret = arm.execution.stop(program_name)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.3.3 返回所有正在运行的程序详细信息

| 方法名  | **all\_running\_programs**() -> tuple\[list, StatusCodeEnum]               |
|------|------------------------------------------|
| 描述   | 返回所有正在运行的程序详细信息 见[程序详细信息][#3.10]         |
| 请求参数 | 无参数                                      |
| 返回值  | list: 运行的程序详细信息列表 [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 执行程序 
ret = arm.execution.start(program_name)
assert ret == StatusCodeEnum.OK

# 获取所有正在运行的程序
ret, programs_list = arm.execution.all_running_programs()
assert ret == StatusCodeEnum.OK
for program in programs_list:
    print(f"正在运行的程序名：{program.program_name}")

# 停止程序
ret = arm.execution.stop(program_name)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.3.4 暂停某个程序的运行

| 方法名  | **pause**(`program_name`: str = '') -> StatusCodeEnum |
|------|-------------------------|
| 描述   | 暂停某个程序的运行               |
| 请求参数 |  `program_name`: str 需要暂停的程序名称, 默认为空字符串，表示暂停当前正在运行的程序或运动指令 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果   |

### 4.3.5 继续运行某个处于暂停状态的程序

| 方法名  | **resume**(`program_name`: str = '') -> StatusCodeEnum  |
|------|---------------------------|
| 描述   | 继续运行某个处于暂停状态的程序           |
| 请求参数 |  `program_name`: str 需要继续运行的程序名称, 默认为空字符串，表示继续运行当前处于暂停状态的程序或运动指令|
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 执行程序 
ret = arm.execution.start(program_name)
assert ret == StatusCodeEnum.OK

# 暂停程序 
ret = arm.execution.pause(program_name)
assert ret == StatusCodeEnum.OK

# 恢复程序
ret = arm.execution.resume(program_name)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.4 程序信息读写

### 4.4.1 获取一个程序中指定序号的机器人Pose点位值

| 方法名  | **program\_pose.read**(`program_name`: str, `index`: int, `program_type`: str = USER\_PROGRAM) -> Tuple\[ProgramPose, StatusCodeEnum]  |
| ---- | -------------------------------------------- |
| 描述   | 获取一个程序中指定序号的Pose的值     |
| 请求参数 | `program_name`: str 指定程序名    `index`: int 指定pose的序号  `program_type`: str 程序类型，默认为USER\_PROGRAM |
| 返回值  | [ProgramPose][#3.17]: 位姿信息  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.program_poses import BLOCK_PROGRAM,USER_PROGRAM

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 读取单个位姿
pose, ret = arm.program_pose.read(program_name, 1,USER_PROGRAM)
assert ret == StatusCodeEnum.OK

# 打印位姿信息
print(
    f"位姿ID：{pose.id}\n"
    f"位姿名称：{pose.name}\n"
    f"位姿类型：{pose.poseData.pt}\n"
    f"X：{pose.poseData.cartData.baseCart.position.x}\n"
    f"Y：{pose.poseData.cartData.baseCart.position.y}\n"
    f"Z：{pose.poseData.cartData.baseCart.position.z}\n"
    f"J1：{pose.poseData.joint.j1}\n"
    f"J2：{pose.poseData.joint.j2}\n"
    f"J3：{pose.poseData.joint.j3}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

### 4.4.2 写入一个程序中指定序号的机器人Pose点位值

| 方法名  | **program\_pose.write**(`program_name`: str, `index`: int, `value`: ProgramPose, `program_type`: str = USER\_PROGRAM) -> StatusCodeEnum|
| ---- | ------------------------------------------------------------------------------------- |
| 描述   | 写入一个程序中指定序号的Pose的值                                                                    |
| 请求参数 | `program_name`: str 指定程序名    `index`: int 指定pose的序号  `value`: [ProgramPose][#3.17] 需更新的新pose值  `program_type`: 程序类型，默认为USER\_PROGRAM  |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.program_poses import BLOCK_PROGRAM,USER_PROGRAM

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 读取单个位姿
pose, ret = arm.program_pose.read(program_name, 1,USER_PROGRAM)
assert ret == StatusCodeEnum.OK

# 修改位姿
pose.comment = "SDK_TEST_COMMENT"
ret = arm.program_pose.write(program_name, 1, pose,USER_PROGRAM)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()
```

### 4.4.3 获取一个程序中所有的机器人Pose点位值

| 方法名  | **program\_pose.read\_all\_poses**(`program_name`: str, `program_type`: str=USER\_PROGRAM) -> Tuple\[List\[ProgramPose], StatusCodeEnum] |
| ---- | ---------------------------------------------- |
| 描述   | 获取一个程序中所有的机器人Pose点位值  |
| 请求参数 | `program_name`: str 指定程序名     `program_type`: str 程序类型，默认为USER\_PROGRAM                            |
| 返回值  | list([ProgramPose][#3.17]): 位姿信息列表： [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.program_poses import BLOCK_PROGRAM,USER_PROGRAM

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 读取所有位姿
poses, ret = arm.program_pose.read_all_poses(program_name,USER_PROGRAM)
assert ret == StatusCodeEnum.OK

# 打印位姿信息
for p in poses:
    print(
        f"位姿ID：{p.id}\n"
        f"位姿名称：{p.name}"
    )

# 结束后断开机器人连接
arm.disconnect()

```

### 4.4.4 写入程序中一个或者多个机器人Pose点位值

| 方法名  | **program\_pose.write\_poses**(`program_name`: str, `poses_to_update`: List\[ProgramPose]) -> StatusCodeEnum  |
|------|---------------------------------------------------------------|
| 描述   | 写入一个程序中一个或者多个的机器人Pose点位值。注意：只能写入已经存在的点位，并不能新增点位                                        |
| 请求参数 | `program_name`: str 指定程序名  `poses_to_update`: List([ProgramPose][#3.17]) 待更新的点位列表                                     |
| 返回值  |[StatusCodeEnum][#3.1]: 函数执行结果             |

示例代码

```python
arm = Arm()
# 连接控制器
assert arm.connect(arm_controller_ip=pytestconfig.inicfg.get('arm_controller_ip')) == StatusCodeEnum.OK
# 程序名
program_name="a"
# 读取第一个位姿
pose_1, res = arm.program_pose.read(program_name, 1)
assert res == StatusCodeEnum.OK
# 读取第三个位姿
pose_3, res = arm.program_pose.read(program_name, 3)
assert res == StatusCodeEnum.OK
# 修改位姿
pose_1.comment = "SDK_TEST_COMMENT__1"
pose_3.comment = "SDK_TEST_COMMENT__3"
pose_3.poseData.cartData.baseCart.position.x=225
pose_3.poseData.cartData.baseCart.position.y=225
pose_3.poseData.cartData.baseCart.position.z=225
# 写回
assert arm.program_pose.write_poses(program_name, [pose_1,pose_3]) == StatusCodeEnum.OK
# 读取全部位姿
poses, res = arm.program_pose.read_all_poses(program_name)
assert res == StatusCodeEnum.OK
assert poses[0].comment == "SDK_TEST_COMMENT__1"
assert poses[2].comment == "SDK_TEST_COMMENT__3"
assert poses[2].poseData.cartData.baseCart.position.x == 225
assert poses[2].poseData.cartData.baseCart.position.y == 225
assert poses[2].poseData.cartData.baseCart.position.z == 225
# 断开连接
arm.disconnect()
```

### 4.4.5 用于在机器人程序中将 Pose 点位在 Cart 坐标系和 Joint 关节坐标系之间相互转换

| 方法名  | **ProgramPoses.convert\_pose**(`pose`: ProgramPose, `from_type`: PoseType, `to_type`: PoseType) -> Tuple\[ProgramPose, StatusCodeEnum]           |
|------|------------------------------------------------------------------------------------|
| 描述   | 用于将程序中机器人位姿P在坐标系类型Cart和Joint之间转换                                                   |
| 请求参数 | `pose`: [ProgramPose][#3.17] 要转换的Pose值 见  `from_type`: [PoseType][#3.6] 转换前的类型  `to_type`: [PoseType][#3.6] 希望转换后的类型       |
| 返回值  | [ProgramPose][#3.17]: 位姿信息  [StatusCodeEnum][#3.1]: 函数执行结果        |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

program_name = 'test'

# 读取单个位姿
pose, ret = arm.program_pose.read(program_name, 1)
assert ret == StatusCodeEnum.OK

# 转换位姿
converted_pose, ret = arm.program_pose.convert_pose(pose, PoseType.CART, PoseType.JOINT)
assert ret == StatusCodeEnum.OK

# 打印位姿信息
print(
    f"位姿ID：{converted_pose.id}\n"
    f"位姿名称：{converted_pose.name}\n"
    f"位姿类型：{converted_pose.poseData.pt}\n"
    f"X：{converted_pose.poseData.cartData.baseCart.position.x}\n"
    f"Y：{converted_pose.poseData.cartData.baseCart.position.y}\n"
    f"Z：{converted_pose.poseData.cartData.baseCart.position.z}\n"
    f"J1：{converted_pose.poseData.joint.j1}\n"
    f"J2：{converted_pose.poseData.joint.j2}\n"
    f"J3：{converted_pose.poseData.joint.j3}\n"
)

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.5 IO信号

### 4.5.1 读取指定类型指定端口IO的值

| 方法名  | **signals.read**(`signal_type`: SignalType, `index`: int) -> tuple\[float, StatusCodeEnum]         |
|------|------------------------------------------------------|
| 描述   | 读取指定类型指定端口IO的值         |
| 请求参数 | `signal_type`: 要读取的IO类型  `index`: 要读取的IO的序号，从1开始 |
| 返回值  | float: IO值，1代表高电平，0代表低电平  [StatusCodeEnum][#3.1]: 函数执行结果     |
| 备注   | UI/UO只能读不能写                |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import SignalType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 读取IO
do_value, ret = arm.signals.read(SignalType.DO, 1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(f"DO 1 状态：{do_value}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.5.2 写指定类型指定端口IO的值

| 方法名  | **signals.write**(`signal_type`: SignalType, `index`: int, `value`: float) -> StatusCodeEnum     |
|------|--------------------------------------------------------------------------------------------------|
| 描述   | 写指定类型指定端口IO的值                    |
| 请求参数 | `signal_type`: SignalType 要写入的IO类型  `index`: int 要写入的IO的序号，从1开始  `value`: float 要写入的值，1代表高电平，0代表低电平，GI/O为整数数值 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |
| 备注   | UI/UO只能读不能写                         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import SignalType, SignalValue

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 写入IO
ret = arm.signals.write(SignalType.DO, 1, SignalValue.ON)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.6 寄存器信息

### 4.6.1 位姿寄存器（PR）

#### 4.6.1.1 获取一个PR寄存器的值

| 方法名  | **register.read\_PR**(`index`: int) -> tuple\[PoseRegister, StatusCodeEnum]        |
|------|-----------------------------------------------------|
| 描述   | 获取一个PR寄存器的值                                  |
| 请求参数 | `index`: int 希望获取的寄存器编号                     |
| 返回值  | [PoseRegister][#3.19] 寄存器信息：见[StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.1.2 写入一个PR寄存器的值

| 方法名  | **register.write\_PR**(`value`: PoseRegister) -> StatusCodeEnum     |
|------|--------------------------------------------------------------------|
| 描述   | 写入一个PR寄存器的值                          |
| 请求参数 | `value`: [PR寄存器信息][#3.19] 需要更新的寄存器信息 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                |

#### 4.6.1.3 删除一个PR寄存器

| 方法名  | **register.delete\_PR**(`index`: int) -> StatusCodeEnum             |
|------|--------------------------------------------------------------------|
| 描述   | 删除一个已存在的PR寄存器的值                   |
| 请求参数 | `index`: int PR寄存器的编号                 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import PoseRegister, Posture, PoseType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加PR寄存器
# 创建位姿
pose_register = PoseRegister()
posture = Posture()
posture.arm_back_front = 1
pose_register.poseRegisterData.posture = posture
pose_register.id = 5
pose_register.poseRegisterData.pt = PoseType.CART
pose_register.poseRegisterData.cartData.position.x = 100
pose_register.poseRegisterData.cartData.position.y = 200
pose_register.poseRegisterData.cartData.position.z = 300
ret = arm.register.write_PR(pose_register)
assert ret == StatusCodeEnum.OK

# 读取PR寄存器
res, ret = arm.register.read_PR(5)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"位姿寄存器ID：{res.id}\n"
    f"位姿类型：{res.poseRegisterData.pt}\n"
    f"X：{res.poseRegisterData.cartData.position.x}\n"
    f"Y：{res.poseRegisterData.cartData.position.y}\n"
    f"Z：{res.poseRegisterData.cartData.position.z}\n"
    )

# 删除PR寄存器
ret = arm.register.delete_PR(5)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.6.2 数值寄存器（R）

#### 4.6.2.1 获取一个R寄存器的值

| 方法名  | **register.read\_R**(`index`: int) -> tuple\[float, StatusCodeEnum]   |
|------|-----------------------------------------------------|
| 描述   | 获取一个R寄存器的值                                         |
| 请求参数 | `index`: int 希望获取的寄存器编号                                   |
| 返回值  | float: 寄存器信值  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.2.2 写入一个R寄存器的值

| 方法名  | **register.write\_R**(`index`: int, `value`: float) -> StatusCodeEnum   |
|------|--------------------------------------------------------------------|
| 描述   | 写入一个R寄存器的值                                                    |
| 请求参数 | `index`: int R寄存器的编号   `value`: float 需要更新的寄存器的值  |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

#### 4.6.2.3 删除一个R寄存器

| 方法名  | **register.delete\_R**(`index`: int) -> StatusCodeEnum                      |
|------|--------------------------------------------------------------------|
| 描述   | 删除一个R寄存器的值                                                    |
| 请求参数 | `index`: int R寄存器的编号                                 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果             |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加R寄存器
ret = arm.register.write_R(5, 8.6)
assert ret == StatusCodeEnum.OK

# 读取R寄存器
res, ret = arm.register.read_R(5)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"R寄存器值：{res}"
    )

# 删除R寄存器
ret = arm.register.delete_R(5)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.6.3 运动寄存器（MR）

#### 4.6.3.1 获取一个MR寄存器的值

| 方法名  | **register.read\_MR**(`index`: int) -> tuple\[int, StatusCodeEnum]     |
|------|-----------------------------------------------------|
| 描述   | 获取一个MR寄存器的值                                         |
| 请求参数 | `index`: int 希望获取的寄存器编号                                   |
| 返回值  | int: 寄存器的值  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.3.2 写入一个MR寄存器的值

| 方法名  | **register.write\_MR**(`index`: int, `value`: int) -> StatusCodeEnum  |
|------|--------------------------------------------------------------------|
| 描述   | 写入一个MR寄存器的值                 |
| 请求参数 | `index`: MR寄存器的编号    `value`: int 需要更新的寄存器的值    |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果               |

#### 4.6.3.3 删除一个MR寄存器

| 方法名  | **register.delete\_MR**(`index`: int) -> StatusCodeEnum        |
|------|--------------------------------------------------------------------|
| 描述   | 删除一个已存在的MR寄存器的值                |
| 请求参数 | `index`: int MR寄存器的编号                |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果             |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import MotionRegister

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加MR寄存器
ret = arm.register.write_MR(5, 8)
assert ret == StatusCodeEnum.OK

# 读取MR寄存器
res, ret = arm.register.read_MR(5)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"MR寄存器值：{res}"
    )

# 删除MR寄存器
ret = arm.register.delete_MR(5)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.6.4 字符串寄存器（SR）

#### 4.6.4.1 获取一个SR寄存器的值

| 方法名  | **register.read\_SR**(`index`: int) -> tuple\[str, StatusCodeEnum]      |
|------|-----------------------------------------------------|
| 描述   | 获取一个SR寄存器的值                                         |
| 请求参数 | `index`: int 希望获取的寄存器编号                                   |
| 返回值  | str: 寄存器的值  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.4.2 写入一个SR寄存器的值

| 方法名  | **register.write\_SR**(`index`: int, `value`: str) -> StatusCodeEnum    |
|------|---------------------------------------------------------|
| 描述   | 写入一个SR寄存器的值                         |
| 请求参数 | `index`: int SR寄存器的编号   `value`: str 需要更新的寄存器值  |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                  |

#### 4.6.4.3 删除一个SR寄存器

| 方法名  | **register.delete\_SR**(`index`: int) -> StatusCodeEnum |
|------|---------------------------------------------------------|
| 描述   | 删除一个SR寄存器                         |
| 请求参数 | `index`: int SR寄存器的编号               |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import StringRegister

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加SR寄存器
ret = arm.register.write_SR(5, 'pytest')
assert ret == StatusCodeEnum.OK

# 读取SR寄存器
res, ret = arm.register.read_SR(5)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"SR寄存器值：{res}"
    )

# 删除SR寄存器
ret = arm.register.delete_SR(5)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.6.5 Modbus寄存器（MH、MI）

兼容性：协作控制器版本 1.4.0（不含）以上支持，工业暂不支持

#### 4.6.5.1 获取一个MH寄存器的值

| 方法名  | **register.read\_MH**(`index`: int) -> tuple\[int, StatusCodeEnum]     |
|------|-----------------------------------------------------|
| 描述   | 获取一个MH寄存器的值                                         |
| 请求参数 | `index`: int 希望获取的寄存器编号                                   |
| 返回值  | int: 寄存器值  [StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.5.2 写入一个MH寄存器的值

| 方法名  | **register.write\_MH**(`index`: int, `value`: int) -> StatusCodeEnum      |
|------|--------------------------------------------------------------------|
| 描述   | 写入一个已存在的MH寄存器的值             |
| 请求参数 | `index`: int MH寄存器的编号   `value`: int 需要更新的寄存器值 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                                              |

#### 4.6.5.3 获取一个MI寄存器的值

| 方法名  | **register.read\_MI**(`index`: int) -> tuple\[int, StatusCodeEnum]       |
|------|-----------------------------------------------------|
| 描述   | 获取一个MI寄存器的值                                         |
| 请求参数 | `index`: int 希望获取的寄存器编号                                   |
| 返回值  | 寄存器值[StatusCodeEnum][#3.1]: 函数执行结果  |

#### 4.6.5.4 写入一个MI寄存器的值

| 方法名  | **register.write\_MI**(`index`: int, `value`: int) -> StatusCodeEnum     |
|------|--------------------------------------------------------------------|
| 描述   | 写入一个已存在的MI寄存器的值           |
| 请求参数 | `index`: int MI寄存器的编号   `value`: int 需要更新的寄存器值 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果       |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import ModbusReg

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 读取MH寄存器
res, ret = arm.register.read_MH(1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"MH寄存器：{res}"
    )

# 写入MH寄存器
assert arm.register.write_MH(1, 16) == StatusCodeEnum.OK

# 读取MI寄存器
res, ret = arm.register.read_MI(1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"MI寄存器：{res}"
    )

# 写入MI寄存器
assert arm.register.write_MI(1, 18) == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.7 轨迹控制

### 4.7.1 设置待执行的离线轨迹文件

| 方法名  | **set\_offline\_trajectory\_file**(`path`: str) -> StatusCodeEnum |
|------|---------------------------------------|
| 描述   | 设置离线轨迹文件          |
| 请求参数 | `path`: str 设置离线轨迹文件程序名，如示例文件A.trajectoryA.trajectory 轨迹文件格式为**文本文件**，说明如下：  - 第1行：6代表6个轴，0.001代表两个点之间间隔1ms ，8093代表一共8093个轨迹点 。  - 第二行：表示6个轴的起始位置 。  - 3-8095行: 表示轨迹点，包括6个轴的位置 、速度 、加速度 、力矩前馈、do端口、do端口的值    - do\_port代表使用的do端口（取值范围1-24）。    - do\_port 为-1， 表示在该位置不会触发IO信号。    - do\_port为1， do\_state为1， 则表明do1 端口会在该位置触发ON 信号    - do\_port为1， do\_state为0， 则表明do1 端口会在该位置触发OFF 信号    |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果     |

### 4.7.2 让机器人以安全速度移动到离线轨迹中的起始点

| 方法名  | **prepare\_offline\_trajectory**() -> StatusCodeEnum |
|------|----------------------------------|
| 描述   | 让机器人以安全速度移动到离线轨迹中的起始点            |
| 请求参数 | 无参数                              |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

### 4.7.3 让机器人开始执行离线轨迹文件

| 方法名  | **execute\_offline\_trajectory**() -> StatusCodeEnum |
|------|----------------------------------|
| 描述   | 让机器人开始执行离线轨迹程序                   |
| 请求参数 | 无参数                              |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置离线轨迹文件
ret = arm.trajectory.set_offline_trajectory_file("torque.trajectory")
assert ret == StatusCodeEnum.OK

# 准备进行离线轨迹运行
ret = arm.trajectory.prepare_offline_trajectory()
assert ret == StatusCodeEnum.OK

# 执行离线轨迹
ret = arm.trajectory.execute_offline_trajectory()
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.8 报警信息

### 4.8.1 重置，用于复位错误

| 方法名  | **reset**() -> StatusCodeEnum    |
|------|------------------------|
| 描述   | 重置，用于复位错误              |
| 请求参数 | 无参数                    |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 重置报警
ret = arm.alarm.reset()
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.8.2 获取所有的活动的报警

| 方法名  | **get\_all\_active\_alarms**() -> tuple\[list, StatusCodeEnum]  |
|------|------------------------------------|
| 描述   | 获取所有的活动的报警                         |
| 请求参数 | 无参数                                |
| 返回值  | list: 报警信息列表[StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取所有的活动的报警
alarms, ret = arm.alarm.get_all_active_alarms()
assert ret == StatusCodeEnum.OK
for alarm in alarms:
    print(alarm)

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.9 文件服务类

### 4.9.1 上传本地文件到机器人

| 方法名  | **file\_manager.upload**(`file_path`: str, `file_type`: str, `overwriting`: bool = False) -> StatusCodeEnum  |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 描述   | 上传本地文件到机器人          |
| 请求参数 | `file_path`: str 需要上传的本地文件的绝对路径 `file_type`: str 上传的文件类型 当前只支持TRAJECTORY、USER\_PROGRAM、BLOCK\_PROGRAM、TRAJECTORY\_CSV、ROBOT\_TMP `overwriting`: bool 是否覆盖写机器人已存在的文件 默认不覆盖写 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果              |
| 备注   | USER\_PROGRAM、BLOCK\_PROGRAM类文件上传只需填写程序名，无需填写后缀           |

示例代码

```python
#!python
from Agilebot.IR.A.file_manager import FileManager
from Agilebot.IR.A.file_manager import TRAJECTORY_CSV, TRAJECTORY, ROBOT_TMP, USER_PROGRAM,BLOCK_PROGRAM
from Agilebot.IR.A.status_code import StatusCodeEnum

# 连接文件管理服务
file_manager = FileManager("10.27.1.254")

# 上传其他文件
ret = file_manager.upload("/home/gbt/test.csv", ROBOT_TMP, True)
assert ret == StatusCodeEnum.OK

# 上传程序（USER_PROGRAM、BLOCK_PROGRAM）
ret = file_manager.upload("/home/gbt/test_prog", USER_PROGRAM, True)
assert ret == StatusCodeEnum.OK
ret = file_manager.upload("/home/gbt/test_block_prog", BLOCK_PROGRAM, True)
assert ret == StatusCodeEnum.OK

# 上传轨迹
ret = file_manager.upload("/home/gbt/test_torque.trajectory", TRAJECTORY, True)
assert ret == StatusCodeEnum.OK

```

### 4.9.2 下载机器人文件到本地

| 方法名  | **file\_manager.download**(`file_name`: str, `file_path`: str, `file_type`: str, `overwriting`: bool=False) -> StatusCodeEnum  |
|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 描述   | 下载机器人文件到本地                                                                                                                                                                               |
| 请求参数 | `file_name`: str 要下载的文件名 无需带后缀  `file_path`: str 下载文件的本地保存路径  `file_type`: str 要下载的文件类型 当前只支持TRAJECTORY、USER\_PROGRAM、TRAJECTORY\_CSV、ROBOT\_TMP，BLOCK\_PROGRAM暂不支持   `overwriting`: bool 是否覆写 如果本地保存路径存在同名文件，是否覆写该同名文件 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.file_manager import FileManager
from Agilebot.IR.A.file_manager import TRAJECTORY
from Agilebot.IR.A.status_code import StatusCodeEnum

# 连接文件管理服务
file_manager = FileManager("10.27.1.254")

# 下载文件
ret = file_manager.download("test_torque", "/home/gbt", file_type=TRAJECTORY)
assert ret == StatusCodeEnum.OK

```

### 4.9.3 删除机器人上的文件

| 方法名  | **file\_manager.delete**(`file_name`: str, `file_type`: str) -> StatusCodeEnum           |
|------|------------------------------------------------------------------------------------------------------|
| 描述   | 删除机器人上的文件    |
| 请求参数 | `file_name`: str 需要删除的文件名 `file_type`: str 需要删除的文件类型 当前只支持TRAJECTORY、USER\_PROGRAM、BLOCK\_PROGRAM、TRAJECTORY\_CSV、ROBOT\_TMP |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果            |

示例代码

```python
#!python
from Agilebot.IR.A.file_manager import FileManager
from Agilebot.IR.A.file_manager import TRAJECTORY_CSV, TRAJECTORY, ROBOT_TMP, USER_PROGRAM,BLOCK_PROGRAM
from Agilebot.IR.A.status_code import StatusCodeEnum

# 连接文件管理服务
file_manager = FileManager("10.27.1.254")

# 删除文件
ret = file_manager.delete("test_torque.trajectory", TRAJECTORY)
assert ret == StatusCodeEnum.OK

# 测试删除用户程序文件
assert file_manager.delete("test", USER_PROGRAM) == StatusCodeEnum.OK

# 测试删除积木块程序
assert file_manager.delete("qa2", BLOCK_PROGRAM) == StatusCodeEnum.OK

```

### 4.9.4 用于在查找符合给定Pattern的文件

| 方法名  | **file\_manager.search**(`pattern`: str, `file_list`: list) -> StatusCodeEnum |
|------|----------------------------------------------|
| 描述   | 查找控制器上符合pattern模式的文件                         |
| 请求参数 | `pattern`: str 文件名称适配字符串  `file_list`: list 适配的文件列表 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                        |

示例代码

```python
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.file_manager import FileManager

file_manager = FileManager("10.27.1.254")
file_list = list()
assert file_manager.search("a*", file_list) == StatusCodeEnum.OK
assert len(file_list) == 1
```

***

## 4.10 坐标系

### 4.10.1 获取用户/工具坐标系摘要信息列表

| 方法名  | **coordinate\_system.get\_coordinate\_list**(`sys_type`: CoordinateSystemType) -> tuple\[UserCoordSummaryList, StatusCodeEnum]    |
|------|-------------------------------------------------------------|
| 描述   | 获取用户/工具坐标系摘要信息列表                                            |
| 请求参数 | `sys_type`: [CoordinateSystemType][#3.22] 坐标系系统类型       |
| 返回值  | [UserCoordSummaryList][#3.23]: 坐标系摘要信息列表  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import CoordinateSystemType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 读取TF列表
tf_list, ret = arm.coordinate_system.get_coordinate_list(CoordinateSystemType.ToolFrame)
assert ret == StatusCodeEnum.OK

# 打印结果
print(f"TF列表t：{tf_list}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.10.2 添加一个用户/工具坐标系

| 方法名  | **coordinate\_system.add**(`sys_type`: CoordinateSystemType) -> tuple\[GeometryPose, StatusCodeEnum]                     |
|------|---------------------------------------------------------|
| 描述   | 添加一个用户/工具坐标系用户/工具坐标系系统                                  |
| 请求参数 | `sys_type`: [CoordinateSystemType][#3.14] 坐标系系统类型        |
| 返回值  | [GeometryPose][#3.14]: 坐标系信息  [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import CoordinateSystemType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加一个坐标系
tf_new, ret = arm.coordinate_system.add(CoordinateSystemType.ToolFrame)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"TF序号：{tf_new.coordinate_info.coordinate_id}\n"
    f"TF名称：{tf_new.coordinate_info.name}\n"
    f"X：{tf_new.position.x}\n"
    f"Y：{tf_new.position.y}\n"
    f"Z：{tf_new.position.z}"
)

# 结束后断开机器人连接
arm.disconnect()

```

### 4.10.3 从当前的用户/工具坐标系系统删除一个用户/工具坐标系

| 方法名  | **coordinate\_system.delete**(`sys_type`: CoordinateSystemType, `coordinate_id`: int) -> StatusCodeEnum       |
|------|---------------------------------------------------------------------------|
| 描述   | 从当前的用户/工具坐标系系统删除一个用户/工具坐标系                                                |
| 请求参数 | `sys_type`: [CoordinateSystemType][#3.14] 坐标系系统类型`coordinate_id`: int 坐标系编号 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                     |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import CoordinateSystemType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加一个坐标系
tf_new, ret = arm.coordinate_system.add(CoordinateSystemType.ToolFrame)
assert ret == StatusCodeEnum.OK

# 删除一个指定的坐标系
ret = arm.coordinate_system.delete(CoordinateSystemType.ToolFrame, 1)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.10.4 从当前的用户/工具坐标系系统更新一个用户/工具坐标系信息

| 方法名  | **coordinate\_system.update**(`sys_type`: CoordinateSystemType, `new_coordinate`: GeometryPose) -> StatusCodeEnum                  |
|------|-----------------------------------------------------------------------------------------------------|
| 描述   | 从当前的用户/工具坐标系系统更新一个用户/工具坐标系                                                                          |
| 请求参数 | `sys_type`: [CoordinateSystemType][#3.14] 坐标系系统类型  `new_coordinate`: [GeometryPose][#3.14] 新坐标系内容 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果                 |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import CoordinateSystemType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 添加一个坐标系
tf_new, ret = arm.coordinate_system.add(CoordinateSystemType.ToolFrame)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"TF序号：{tf_new.coordinate_info.coordinate_id}\n"
    f"TF名称：{tf_new.coordinate_info.name}\n"
    f"X：{tf_new.position.x}\n"
    f"Y：{tf_new.position.y}\n"
    f"Z：{tf_new.position.z}"
)

# 更新一个指定的坐标系
tf_new.coordinate_info.comment = "test"
tf_new.position.x = 20
ret = arm.coordinate_system.update(CoordinateSystemType.ToolFrame, tf_new)
assert ret == StatusCodeEnum.OK

# 结束后断开机器人连接
arm.disconnect()

```

### 4.10.5 从当前的用户/工具坐标系系统获取一个用户/工具坐标系信息

| 方法名  | **coordinate\_system.get**(`sys_type`: CoordinateSystemType, `coordinate_id`: int) -> tuple\[GeometryPose, StatusCodeEnum]         |
|------|-----------------------------------------------------------------------------|
| 描述   | 从当前的用户/工具坐标系系统获取一个指定的用户/工具坐标系                                               |
| 请求参数 | `sys_type`: [CoordinateSystemType][#3.22] 坐标系系统类型  `coordinate_id`: int 坐标系编号 |
| 返回值  | [GeometryPose][#3.26]: 坐标系信息  [StatusCodeEnum][#3.1]: 函数执行结果                      |

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_types import CoordinateSystemType

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 获取指定工具坐标系
tf, ret = arm.coordinate_system.get(CoordinateSystemType.ToolFrame, 1)
assert ret == StatusCodeEnum.OK

# 打印结果
print(
    f"TF序号：{tf.coordinate_info.coordinate_id}\n"
    f"TF名称：{tf.coordinate_info.name}\n"
    f"X：{tf.position.x}\n"
    f"Y：{tf.position.y}\n"
    f"Z：{tf.position.z}"
)

# 结束后断开机器人连接
arm.disconnect()

```

***

## 4.11 Modbus 相关功能

备注：Modbus 相关功能和示教器上的总线配置冲突，不可同时使用

### 4.11.1 获取指定通道的指定从机ID的 Modbus 从机实例

| 方法名  | **modbus.get\_slave**(`channel`: ModbusChannel, `slave_id`: int, `master_id`: int = 0) -> 'Modbus.Slave' |
|------|-----------------------------------------------------------------------------|
| 描述   | 获取指定通道的指定从机ID的 Modbus 从机实例                      |
| 请求参数 | `channel`: [ModbusChannel][#3.30] Modbus 通道  `slave_id`: 从机ID  `master_id`: 主机ID |
| 返回值  | Modbus.Slave: Modbus 从机实例|

### 4.11.2 读取从机modbus线圈寄存器

| 方法名  | **slave.read\_coils**(`address`: int, `number`: int ) -> tuple\[list\[int], StatusCodeEnum] |
|------|-------------------------------------------------------|
| 描述   | 读取从机modubus线圈寄存器                      |
| 请求参数 | `address`: int 寄存器地址  `number`: int 寄存器数量(最大为120个) |
| 返回值  | list\[int]：寄存器值  [StatusCodeEnum][#3.1]: 函数执行结果|

### 4.11.3 写入从机modbus线圈寄存器

| 方法名  | **slave.write\_coils**(`address`: int, `value`: list\[int]) -> StatusCodeEnum |
|------|----------------------------------------------------|
| 描述   | 写入从机modubus线圈寄存器                      |
| 请求参数 | `address`: int 寄存器地址  `value`: list\[int] 寄存器值|
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.11.4 读取从机modbus保持寄存器

| 方法名  | **slave.read\_holding\_regs**(`address`: int, `number`: int ) -> tuple\[list\[int], StatusCodeEnum] |
|------|--------------------------------------------------|
| 描述   | 读取从机modubus保持寄存器                      |
| 请求参数 |  `address`: int 寄存器地址  `number`: int 寄存器数量(最大为120个) |
| 返回值  | list\[int]：寄存器值[StatusCodeEnum][#3.1]: 函数执行结果|

### 4.11.5 写入从机modbus保持寄存器

| 方法名  | **slave.write\_holding\_regs**(`address`: int, `value`: list\[int]) -> StatusCodeEnum |
|------|-----------------------------------------------|
| 描述   | 写入从机modubus保持寄存器                      |
| 请求参数 | `address`: int 寄存器地址  `value`: list\[int] 寄存器值|
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.11.6 读取从机modbus离散寄存器

| 方法名  | **slave.read\_discrete\_inputs**(`address`: int, `number`: int ) -> tuple\[list\[int], StatusCodeEnum] |
|------|-----------------------------------------------------------------------------|
| 描述   | 读取从机modubus离散寄存器                      |
| 请求参数 |  `address`: int 寄存器地址  `number`: int 寄存器数量(最大为120个) |
| 返回值  | list\[int]：寄存器值[StatusCodeEnum][#3.1]: 函数执行结果|

### 4.11.7 读取从机modbus输入寄存器

| 方法名  | **slave.read\_input\_regs**(`address`: int, `number`: int ) -> tuple\[list\[int], StatusCodeEnum] |
|------|-----------------------------------------------------------------------------|
| 描述   | 读取从机modubus输入寄存器                      |
| 请求参数 |  `address`: int 寄存器地址  `number`: int 寄存器数量(最大为120个) |
| 返回值  | list\[int]：寄存器值[StatusCodeEnum][#3.1]: 函数执行结果|

示例代码

```python
#!python
from Agilebot.IR.A.arm import Arm
from Agilebot.IR.A.status_code import StatusCodeEnum
from Agilebot.IR.A.sdk_classes import SerialParams
from Agilebot.IR.A.sdk_types import ModbusChannel

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置modbus参数
params = SerialParams(channel=ModbusChannel.CONTROLLER_TCP_TO_485,ip='10.27.1.80',port=502)
id, ret_code = arm.modbus.set_parameter(params)
assert ret_code == StatusCodeEnum.OK

# 创建从站
slave = arm.modbus.get_slave(ModbusChannel.CONTROLLER_TCP_TO_485, 1, 1)

# 写入
value = [1,2,3,4]
assert slave.write_coils(0,value) == StatusCodeEnum.OK
assert slave.write_holding_regs(0,value) == StatusCodeEnum.OK

# 读取
res, ret = slave.read_coils(0,4)
assert ret == StatusCodeEnum.OK
print(f"读取的线圈值：{res}")
res, ret = slave.read_holding_regs(0,4)
assert ret == StatusCodeEnum.OK
print(f"读取的寄存器值：{res}")
res, ret = slave.read_input_regs(0,4)
assert ret == StatusCodeEnum.OK
print(f"读取的输入寄存器值：{res}")
res, ret = slave.read_discrete_inputs(0,4)
assert ret == StatusCodeEnum.OK
print(f"读取的离散输入值：{res}")

# 结束后断开机器人连接
arm.disconnect()

```

### 4.11.8 设置串口通讯参数

| 方法名  | **modbus.set\_parameter**(`param`: SerialParams) -> tuple\[int, StatusCodeEnum] |
|------|---------------------------------------------|
| 描述   | 读取串口线圈寄存器                      |
| 请求参数 | `param`: SerialParams 串口通讯参数 |
| 返回值  | int: 通道ID  [StatusCodeEnum][#3.1]: 函数执行结果|

### 4.11.9 获取串口通讯参数

| 方法名  | **modbus.get\_parameter**(`channel`: ModbusChannel, `master_id`: int = 1) -> tuple\[SerialParams, StatusCodeEnum] |
|------|---------------------------------------------|
| 描述   | 读取串口线圈寄存器                      |
| 请求参数 | `channel`: [ModbusChannel][#3.30] Modbus 通道  `master_id`: int 主机ID |
| 返回值  | SerialParams: 串口通讯参数  [StatusCodeEnum][#3.1]: 函数执行结果|

## 4.12 BasScript脚本程序类

| 方法名  | **BasScript**(`name`) |
| ---- | ------------------------- |
| 描述   | 对应示教器程序编写中的程序指令 |
| 请求参数 | `name`：脚本程序名 |
| 兼容性   | 协作机器人控制器版本 1.4.1 及以上版本，工业机器人不支持         |

### 4.12.1 MoveJoint指令

| 方法名  | **BasScript.move\_joint**(`pose_type`, `pose_index`, `speed_type`, `speed_value`, `smooth_type`, `smooth_distance`, `extra_param`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的MoveJoint指令                      |
| 请求参数 | `pose_type`：位姿类型  `pose_index`：位姿索引  `speed_type`：速度类型  `speed_value`：速度值  `smooth_type`：平滑类型  `smooth_distance`：平滑距离  `extra_param`：附加参数 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.2 MoveLine指令

| 方法名  | **BasScript.move\_line**(`pose_type`, `pose_index`, `speed_type`, `speed_value`, `smooth_type`, `smooth_distance`, `extra_param`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的MoveLine指令                      |
| 请求参数 | `pose_type`：位姿类型  `pose_index`：位姿索引  `speed_type`：速度类型  `speed_value`：速度值  `smooth_type`：平滑类型  `smooth_distance`：平滑距离  `extra_param`：附加参数 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.3 MoveCircle指令

| 方法名  | **BasScript.move\_circle**(`pose_type1`, `pose_index1`, `pose_type2`, `pose_index2`, `speed_type`, `speed_value`, `smooth_type`, `smooth_distance`, `extra_param`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的MoveCircle指令                      |
| 请求参数 | `pose_type1`：第一个位姿类型  `pose_index1`：第一个位姿索引  `pose_type2`：第二个位姿类型  `pose_index2`：第二个位姿索引  `speed_type`：速度类型  `speed_value`：速度值  `smooth_type`：平滑类型  `smooth_distance`：平滑距离  `extra_param`：附加参数 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.4 LogiIf指令

| 方法名  | **BasScript.logi\_if**(`param1`, `index`, `param2`, `value`, `operator`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的IF逻辑语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `operator`：逻辑运算符 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.5 LogiElseIf指令

| 方法名  | **BasScript.logi\_else\_if**(`param1`, `index`, `param2`, `value`, `operator`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ELIF逻辑语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `operator`：逻辑运算符 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.6 LogiElse指令

| 方法名  | **BasScript.logi\_else**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ELSE逻辑语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.7 LogiEndIf指令

| 方法名  | **BasScript.logi\_end\_if**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ENDIF逻辑语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.8 LogiWhile指令

| 方法名  | **BasScript.logi\_while**(`param1`, `index`, `param2`, `value`, `operator`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的WHILE逻辑语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `operator`：逻辑运算符 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.9 LogiEndWhile指令

| 方法名  | **BasScript.logi\_end\_while**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ENDWHILE逻辑语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.10 LogiSwitch指令

| 方法名  | **BasScript.logi\_switch**(`param`, `index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SWITCH逻辑语句                      |
| 请求参数 | `param`：参数  `index`：索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.11 LogiCase指令

| 方法名  | **BasScript.logi\_case**(`param`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的CASE逻辑语句                      |
| 请求参数 | `param`：参数  `value`：值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.12 LogiDefault指令

| 方法名  | **BasScript.logi\_default**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的DEFAULT逻辑语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.13 LogiEndSwitch指令

| 方法名  | **BasScript.logi\_end\_switch**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ENDSWITCH逻辑语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.14 LogiGoto指令

| 方法名  | **BasScript.logi\_goto**(`index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的GOTO跳转语句                      |
| 请求参数 | `index`：目标标签的索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.15 LogiLabel指令

| 方法名  | **BasScript.logi\_label**(`index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的LABEL标签语句                      |
| 请求参数 | `index`：标签的索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.16 LogiSkipCondition指令

| 方法名  | **BasScript.logi\_skip\_condition**(`param1`, `index`, `param2`, `value`, `operator`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SKIP CONDITION跳转语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `operator`：逻辑运算符 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.17 LogiBreak指令

| 方法名  | **BasScript.logi\_break**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的BREAK语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.18 LogiContinue指令

| 方法名  | **BasScript.logi\_continue**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的CONTINUE语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.19 AssignValue指令

| 方法名  | **BasScript.assign\_value**(`param1`, `index`, `param2`, `value`, `opt_index`, `opt_value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ASSIGN赋值语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `opt_index`：可选索引  `opt_value`：可选值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.20 Wait指令

| 方法名  | **BasScript.wait**(`param1`, `index`, `param2`, `value`, `operator`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的WAIT COND等待条件语句                      |
| 请求参数 | `param1`：第一个参数  `index`：索引  `param2`：第二个参数  `value`：值  `operator`：逻辑运算符 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.21 WaitTime指令

| 方法名  | **BasScript.wait\_time**(`param`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的WAIT TIME等待时间语句                      |
| 请求参数 | `param`：参数  `value`：时间值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.22 Pause指令

| 方法名  | **BasScript.pause**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的PAUSE暂停语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.23 Abort指令

| 方法名  | **BasScript.abort**() |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的ABORT终止语句                      |
| 请求参数 | 无 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.24 Call指令

| 方法名  | **BasScript.call**(`name`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的CALL同步调用程序                      |
| 请求参数 | `name`：程序名 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.25 Run指令

| 方法名  | **BasScript.run**(`name`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的RUN异步调用程序                      |
| 请求参数 | `name`：程序名 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.26 Load指令

| 方法名  | **BasScript.load**(`param`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的LOAD载入程序                      |
| 请求参数 | `param`：参数  `value`：值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.27 Unload指令

| 方法名  | **BasScript.unload**(`param`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的UNLOAD卸载程序                      |
| 请求参数 | `param`：参数  `value`：值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.28 Exec指令

| 方法名  | **BasScript.exec**(`param`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的EXEC执行程序                      |
| 请求参数 | `param`：参数  `value`：值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.29 SocketOpen指令

| 方法名  | **BasScript.socket\_open**(`index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SOCKET OPEN打开socket连接                      |
| 请求参数 | `index`：SK寄存器序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.30 SocketClose指令

| 方法名  | **BasScript.socket\_close**(`index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SOCKET CLOSE关闭socket连接                      |
| 请求参数 | `index`：SK寄存器序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.31 SocketConnect指令

| 方法名  | **BasScript.socket\_connect**(`index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SOCKET CONNECT连接socket                      |
| 请求参数 | `index`：SK寄存器序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.32 SocketSend指令

| 方法名  | **BasScript.socket\_send**(`index`, `msg_type`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SOCKET SEND发送数据                      |
| 请求参数 | `index`：SK寄存器序号  `msg_type`：消息类型  `value`：消息内容或序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.33 SocketRecv指令

| 方法名  | **BasScript.socket\_recv**(`index`, `msg_length`, `msg_type`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SOCKET RECV接收数据                      |
| 请求参数 | `index`：SK寄存器序号  `msg_length`：消息长度  `msg_type`：消息类型  `value`：消息内容或序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.34 ModbusReadMH指令

| 方法名  | **BasScript.modbus\_read\_MH**(`index`, `id`, `address`, `length`, `r_index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的READ\_MH读取Modbus保持寄存器                      |
| 请求参数 | `index`：通道序号  `id`：Modbus ID  `address`：寄存器地址  `length`：寄存器长度  `r_index`：R寄存器序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.35 ModbusReadMI指令

| 方法名  | **BasScript.modbus\_read\_MI**(`index`, `id`, `address`, `length`, `r_index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的READ\_MI读取Modbus输入寄存器                      |
| 请求参数 | index：通道序号  `id`：Modbus ID  `address`：寄存器地址  `length`：寄存器长度  `r_index`：R寄存器序号 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.36 ModbusWriteMH指令

| 方法名  | **BasScript.modbus\_write\_MH**(`index`, `id`, `address`, `length`, `value_type`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的WRITE\_MH写入Modbus保持寄存器                      |
| 请求参数 | `index`：通道序号  `id`：Modbus ID  `address`：寄存器地址  `length`：寄存器长度  `value_type`：值类型  `value`：值或索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.37 VisionFind指令

| 方法名  | **BasScript.vision\_find**(`name`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的VISION FIND寻找视觉程序                      |
| 请求参数 | `name`：视觉程序名称 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.38 VisionGetOffset指令

| 方法名  | **BasScript.vision\_get\_offset**(`name`, `index`, `label_index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的VISION GET OFFSET获取视觉程序偏移量                      |
| 请求参数 | `name`：视觉程序名称  `index`：视觉寄存器索引  `label_index`：标签索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.39 VisionGetQuantity指令

| 方法名  | **BasScript.vision\_get\_quantity**(`name`, `index`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的VISION GET QUANTITY获取视觉程序结果                      |
| 请求参数 | `name`：视觉程序名称  `index`：R寄存器索引 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.40 SetParam指令

| 方法名  | **BasScript.set\_param**(`type`, `value_type`, `value`) |
|------|-----------------------------------------------------------------------------|
| 描述   | 对应示教器程序编写中的SET PARAM设置参数                      |
| 请求参数 | `type`：参数类型  `value_type`：值类型  `value`：值 |
| 返回值  |  [StatusCodeEnum][#3.1]: 函数执行结果 |

### 4.12.41 ExtraParam类

| 方法名  | **ExtraParam**() |
| ---- | ------------------------- |
| 描述   | 额外参数类，用于构建复杂的机器人控制命令 |
| 请求参数 | 无 |
| 返回值  | 无 |

#### 4.12.41.1 设置加速度

| 方法名  | **ExtraParam.acceleration**(`value`) |
| ---- | ------------------------- |
| 描述   | 设置加速度，范围为 1~120 |
| 请求参数 | `value`：加速度值（浮点数） |
| 返回值  | 无 |

#### 4.12.41.2 设置 RTCP 参数

| 方法名  | **ExtraParam.rctp**() |
| ---- | ------------------------- |
| 描述   | 设置 RTCP 参数 |
| 请求参数 | 无 |
| 返回值  | 无 |

#### 4.12.41.3 设置帧偏移

| 方法名  | **ExtraParam.offset**(`index`) |
| ---- | ------------------------- |
| 描述   | 设置帧偏移 |
| 请求参数 | `index`：偏移索引（整数） |
| 返回值  | 无 |

#### 4.12.41.4 设置时间基准运行或赋值

| 方法名  | **ExtraParam.tb**(`second`, `type`, `name`=None, `index`=None, `status`=None) |
| ---- | ------------------------- |
| 描述   | 设置时间基准运行或赋值 |
| 请求参数 | `second`：秒数（整数）  `type`：执行类型（字符串）  `name`：名称（用于运行，字符串）  `index`：索引（用于赋值，整数）  `status`：状态（用于赋值，字符串） |
| 返回值  | 无 |

#### 4.12.41.5 设置跳转

| 方法名  | **ExtraParam.skip**(`index`) |
| ---- | ------------------------- |
| 描述   | 设置跳转 |
| 请求参数 | `index`：标签索引（整数） |
| 返回值  | 无 |

### 4.12.42 JUMP指令

#### 4.12.42.1 JUMP

| 方法名  | **move\_jump**(`pose_type`, `pose_index`, `speed_value`, `speed_ratio`, `lim_Z_type`, `lim_Z_value`, `smooth_type`, `smooth_distance`=0.0, `extra_param`=None) |
| ---- | ------------------------- |
| 描述   | 机器人点对点移动到指定位置 |
| 请求参数 | `pose_type`：目标位姿存储类型（`MovePoseType`，目前支持PR寄存器）  `pose_index`：目标位置的索引（整数，表示在控制器上的PR寄存器中的位置）  `speed_value`：移动速度的值（浮点数，单位为mm/s）  `speed_ratio`：移动速度的比率（浮点数，单位为%，范围为0~100）  `lim_Z_type`：Z轴限制的类型（`SpeedType`，可以是MR寄存器或数值VALUE）  `lim_Z_value`：Z轴限制的值（如果`lim_Z_type`为MR寄存器，表示MR寄存器序号；如果为数值VALUE，表示Z轴限制的值，单位为mm/s，范围为0~100）  `smooth_type`：平滑类型（`SmoothType`，可以是FINE或SMOOTH\_DISTANCE）  `smooth_distance`：平滑距离（浮点数，仅在`smooth_type`为SMOOTH\_DISTANCE时生效，范围为0~1000）  `extra_param`：额外参数（`ExtraParam`，用于设置MOVE指令的额外参数，可选） |
| 返回值  | 操作结果的状态码（`StatusCodeEnum`） |

#### 4.12.42.2 JUMP3

| 方法名  | **move\_jump3**(`pose_type`, `pose_index`, `speed_value`, `speed_ratio`, `smooth_type`, `smooth_distance`=0.0, `extra_param`=None) |
| ---- | ------------------------- |
| 描述   | 机器人点对点移动到指定位置 |
| 请求参数 | `pose_type`：目标位姿存储类型（`MovePoseType`，目前支持PR寄存器）  `pose_index`：3个目标位置的索引（列表，包含3个整数，表示在控制器上的PR寄存器中的位置）  `speed_value`：移动速度的值（浮点数，单位为mm/s）  `speed_ratio`：移动速度的比率（浮点数，单位为%，范围为0~100）  `smooth_type`：平滑类型（`SmoothType`，可以是FINE或SMOOTH\_DISTANCE）  `smooth_distance`：平滑距离（浮点数，仅在`smooth_type`为SMOOTH\_DISTANCE时生效，范围为0~1000）  `extra_param`：额外参数（`ExtraParam`，用于设置MOVE指令的额外参数，可选） |
| 返回值  | 操作结果的状态码（`StatusCodeEnum`） |

#### 4.12.42.3 JUMP3CP

| 方法名  | **move\_jump3cp**(`pose_type`, `pose_index`, `speed_value`, `smooth_type`, `smooth_distance`=0.0, `extra_param`=None) |
| ---- | ------------------------- |
| 描述   | 机器人点对点移动到指定位置 |
| 请求参数 | `pose_type`：目标位姿存储类型（`MovePoseType`，目前支持PR寄存器）  `pose_index`：3个目标位置的索引（列表，包含3个整数，表示在控制器上的PR寄存器中的位置）  `speed_value`：移动速度的值（浮点数，单位为mm/s）  `smooth_type`：平滑类型（`SmoothType`，可以是FINE或SMOOTH\_DISTANCE）  `smooth_distance`：平滑距离（浮点数，仅在`smooth_type`为SMOOTH\_DISTANCE时生效，范围为0~1000）  `extra_param`：额外参数（`ExtraParam`，用于设置MOVE指令的额外参数，可选） |
| 返回值  | 操作结果的状态码（`StatusCodeEnum`） |

## 4.13 机器人示教运动

### 4.13.1 控制机器人以连续运动或者根据进给量运动

| 方法名  | **jogging.move**(`aj_num`: int, `move_mode`: MoveMode = None, `step_length`: float = 0) -> StatusCodeEnum       |
|------|---------------------------------------------------------|
| 描述   | 控制机器人以连续运动或者根据进给量运动                |
| 请求参数 | `aj_num`: int 填写数值1-6  数值1~6对应关系根据当前示教的坐标系来决定  关节坐标系下 关节值号\[1 ~ 6] 笛卡尔坐标系下x, y, z, rx, ry, rz  `move_mode`: [MoveMode][#3.32] 机械臂运动模式 增量运动 or 连续运动   `step_length`: float 单次步进量，单位为mm或°, 不给值即不修改步进值|
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果       |

示例代码

```python
from Agilebot.IR.A.arm import Arm, SoftModeEnum
from Agilebot.IR.A.jogging.jogging import MoveMode
from Agilebot.IR.A.sdk_types import ParamType, CoordType
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置软模式
arm.set_soft_mode(SoftModeEnum.MANUAL_LIMIT)
assert arm.get_soft_mode()[1] == SoftModeEnum.MANUAL_LIMIT

# 设置关节坐标系
assert arm.motion.set_param(name=ParamType.TCS, value=CoordType.JOINT) == StatusCodeEnum.OK

# jogging step move 点动关节坐标系下的关节1
assert arm.jogging.move(1, MoveMode.Stepping, 5) == StatusCodeEnum.OK

arm.disconnect()
```

### 4.13.2 停止机器人jog运动

| 方法名  | **jogging.stop**()     |
|------|------------------------|
| 描述   | 终止机器人jog运动             |
| 请求参数 | 无参数                    |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果  |

示例代码

```python
from Agilebot.IR.A.arm import Arm, SoftModeEnum
from Agilebot.IR.A.jogging.jogging import MoveMode
from Agilebot.IR.A.sdk_types import ParamType, CoordType
from Agilebot.IR.A.status_code import StatusCodeEnum

# 初始化Arm类
arm = Arm()
# 连接控制器
ret = arm.connect("10.27.1.254")
# 检查是否连接成功
assert ret == StatusCodeEnum.OK

# 设置软模式
arm.set_soft_mode(SoftModeEnum.MANUAL_LIMIT)
assert arm.get_soft_mode()[1] == SoftModeEnum.MANUAL_LIMIT

# 设置关节坐标系
assert arm.motion.set_param(name=ParamType.TCS, value=CoordType.JOINT) == StatusCodeEnum.OK

# jogging step move 点动关节坐标系下的关节1
assert arm.jogging.move(1, MoveMode.Continuous) == StatusCodeEnum.OK
arm.jogging.stop()

arm.disconnect()
```

## 4.14 订阅机器人状态值

| 方法名  | **subscribe**(`topic_list`: List\[HWState] = None, `io_topic`: List\[Tuple\[IOTopic, int]] = None) -> StatusCodeEnum       |
|------|------------------------------------------------------------------|
| 描述   | 开启订阅机器人状态  支持订阅的机器人状态见[HWState枚举][#3.15]                |
| 请求参数 | `topic_list`: [HWState枚举][#3.15] 默认订阅(机器人JOINT关节值、笛卡尔TCP位置、TF、UF、机器人运行状态、机器人运行速度)  `io_topic`: 自定义需要订阅的IO信号列表 |
| 返回值  | [StatusCodeEnum][#3.1]: 函数执行结果         |

示例代码

```python
#!python
from Agilebot.IR.A.hardware_state import *

# 初始化订阅
hw_state = HardwareState("10.27.1.254")

# 订阅机器人状态
ret = hw_state.subscribe()
assert ret == StatusCodeEnum.OK

# 打印订阅的消息
for i in range(10):
    print(hw_state.recv())

# 关闭订阅
hw_state.unsubscribe()

# 订阅IO状态
io_topic = []
io_topic.extend([(IOTopic.DO, i) for i in range(1, 2)])
ret = hw_state.subscribe(io_topic=io_topic)
assert ret == StatusCodeEnum.OK

# 打印订阅的消息
for i in range(10):
    print(hw_state.recv())

# 关闭订阅
hw_state.unsubscribe()

```
