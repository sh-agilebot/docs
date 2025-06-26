---
url: /zh/1-python/3-struct.md
---
# 3 数据结构

## 3.1 StatusCodeEnum

### 说明

接口返回状态码

备注：如发现未在说明书里显示的返回码，需要查看机器人故障码表或者根据返回值的字面意思理解

### 导入

```python
from Agilebot.IR.A.status_code import StatusCodeEnum
```

### 字段

| **名称**                                 | **枚举值** | **描述**                         |
|----------------------------------------|---------|--------------------------------|
| `OK`                                   | 0       | 成功                             |
| `INCOMPATIBLE_VERSION`                 | -1      | 版本不兼容                          |
| `CONNECTION_TIMEOUT`                   | -3      | 连接超时                           |
| `INTERFACE_NOTIMPLEMENTED`             | -4      | 当前控制器该接口未实现                    |
| `INDEX_OUT_OF_RANGE`                   | -5      | 索引下标越界                         |
| `UNSUPPORTED_FILETYPE`                 | -6      | 不支持的文件类型                       |
| `UNSUPPORTED_PARAMETER`                | -7      | 不支持的机器人参数                      |
| `UNSUPPORTED_SIGNAL_TYPE`              | -8      | 不支持的IO信号类型                     |
| `PROGRAM_NOT_FOUND`                    | -9      | 找不到对应的程序                       |
| `PROGRAM_POSE_NOT_FOUND`               | -10     | 找不到对应的程序点位                     |
| `WRITE_PROGRAM_POSE_FAILED`            | -11     | 更新写入程序点位失败                     |
| `GET_ALARM_CODE_FAILED`                | -12     | 访问报警服务获取报警码失败                  |
| `WRONG_POSITION_INFO`                  | -13     | 控制器返回错误的点位信息                   |
| `UNSUPPORTED_TRATYPE`                  | -14     | 不支持的运动类型                       |
| `INVALID_DH_LIST`                      | -15     | 错误的变换参数列表，请联系开发人员              |
| `INTERVAL_PORTS_MUST_NOTNONE`          | -16     | 时间间隔和输出端口列表和电平持续时间必须非空         |
| `INVALID_IP_ADDRESS`                   | -17     | 无效的IP地址                        |
| `INVALID_DH_PARAMETERS`                | -18     | 无效的DH参数                        |
| `INVALID_PAYLOAD_INFO`                 | -19     | 无效的负载信息                        |
| `INVALID_FLYSHOT_CONFIG`               | -20     | 无效的飞拍配置参数                      |
| `FAILED_TO_DOWNLOAD_SAME_NAME_FILE`    | -21     | 因重名不允许覆写                       |
| `FAILED_TO_CONVERT_CART_TO_JOINT`      | -22     | 转换笛卡尔坐标失败                      |
| `FAILED_TO_GET_ALL_INVERSE_KINEMATICS` | -23     | 获取一个回转数内的八组解失败                 |
| `COORDINATE_LIMIT_EXCEEDED`            | -24     | 坐标系个数上限为10个 坐标系ID合法范围值是\[1, 10] |
| `FILE_NOTEXIST`                        | -25     | 文件不存在                          |
| `INVALID_IO_LIST_PARAMETERS`           | -26     | 无效的IO列表参数                      |
| `CONTROLLER_ERROR`                     | -254    | 控制器错误，详情请联系开发人员                |
| `SERVER_ERR`                           | -255    | 其他原因                           |

## 3.2 RobotStatusEnum

### 说明

机器人运行状态

### 导入

```python
from Agilebot.IR.A.sdk_types import RobotStatusEnum
```

### 字段

| **名称**                   | **枚举值** | **描述**          |
|--------------------------|---------|-----------------|
| `ROBOT_UNKNOWN`          | -1      | 未知状态            |
| `ROBOT_IDLE`             | 0       | 机器人空闲           |
| `ROBOT_RUNNING`          | 1       | 机器人运行中          |
| `ROBOT_TEACHING`         | 2       | 机器人示教中          |
| `ROBOT_IDLE_TO_RUNNING`  | 101     | 机器人中间状态 空闲转换为运行 |
| `ROBOT_IDLE_TO_TEACHING` | 102     | 机器人中间状态 空闲转换为示教 |
| `ROBOT_RUNNING_TO_IDLE`  | 103     | 机器人中间状态 运行转换为空闲 |
| `ROBOT_TEACHING_TO_IDLE` | 104     | 机器人中间状态 示教转换为空闲 |

## 3.3 CtrlStatusEnum

### 说明

控制器运行状态

### 导入

```python
from Agilebot.IR.A.sdk_types import CtrlStatusEnum
```

### 字段

| 名称                         | 枚举值 | 描述              |
|----------------------------|-----|-----------------|
| `CTRL_UNKNOWN`             | -1  | 未知的控制器状态        |
| `CTRL_INIT`                | 0   | 控制器初始化          |
| `CTRL_ENGAGED`             | 1   | 控制器使能           |
| `CTRL_ESTOP`               | 2   | 控制器急停           |
| `CTRL_TERMINATED`          | 3   | 控制器中止           |
| `CTRL_ANY_TO_ESTOP`        | 101 | 控制器中间状态 其他转换为急停 |
| `CTRL_ESTOP_TO_ENGAGED`    | 102 | 控制器中间状态 急停到使能   |
| `CTRL_ESTOP_TO_TERMINATED` | 103 | 控制器中间状态 急停到中止   |

## 3.4 ServoStatusEnum

### 说明

伺服控制器状态

### 导入

```python
from Agilebot.IR.A.sdk_types import ServoStatusEnum
```

### 字段

| 名称                 | 枚举值 | 描述         |
|--------------------|-----|------------|
| `SERVO_UNKNOWN`    | -1  | 未知的伺服控制器状态 |
| `SERVO_IDLE`       | 1   | 伺服控制器空闲    |
| `SERVO_RUNNING`    | 2   | 伺服控制器运行中   |
| `SERVO_DISABLE`    | 3   | 伺服控制器关闭    |
| `SERVO_WAIT_READY` | 4   | 伺服控制器等待就绪  |
| `SERVO_WAIT_DOWN`  | 5   | 伺服控制器等待关闭  |
| `SERVO_INIT`       | 10  | 伺服控制器初始化   |

## 3.5 SoftModeEnum

### 说明

机器人PC状态模式状态

### 导入

```python
from Agilebot.IR.A.sdk_types import SoftModeEnum
```

### 字段

| 名称             | 枚举值 | 描述     |
|----------------|-----|--------|
| `UNKNOWN`      | 0   | 未知     |
| `AUTO`         | 1   | 自动模式   |
| `MANUAL_LIMIT` | 2   | 手动限速模式 |
| `MANUAL`       | 3   | 手动模式   |

## 3.6 PoseType

### 说明

机器人参数类型

### 导入

```python
from Agilebot.IR.A.sdk_types import PoseType
```

### 字段

| 名称         | 枚举值 | 描述        |
|-------------|-----|-----------|
| `JOINT`     | 0   | 关节空间      |
| `CART`      | 1   | 笛卡尔坐标      |

## 3.7 TCSType

### 说明

坐标系类型

### 导入

```python
from Agilebot.IR.A.sdk_types import TCSType
```

### 字段

| 名称         | 枚举值 | 描述        |
|-------------|-----|-----------|
| `JOINT`     | 0   | 关节空间      |
| `BASE`      | 1   | 基坐标系      |
| `WORLD`     | 2   | 世界坐标系     |
| `USER`      | 3   | 用户坐标系     |
| `TOOL`      | 4   | 工具坐标系     |
| `RTCP_USER` | 5   | RTCP用户坐标系 |
| `RTCP_TOOL` | 6   | RTCP工具坐标系 |

## 3.8 Joint

### 说明

描述机器人关节位置的数据结构

### 导入

```python
from Agilebot.IR.A.sdk_classes import Joint
```

### 属性

| 属性   | 类型      | 描述    |
|------|---------|-------|
| `j1` | `float` | 关节1的值 |
| `j2` | `float` | 关节2的值 |
| `j3` | `float` | 关节3的值 |
| `j4` | `float` | 关节4的值 |
| `j5` | `float` | 关节5的值 |
| `j6` | `float` | 关节6的值 |
| `j7` | `float` | 关节7的值 |
| `j8` | `float` | 关节8的值 |
| `j9` | `float` | 关节9的值 |

## 3.9 Position

### 说明

描述机器人笛卡尔位姿的数据结构

### 导入

```python
from Agilebot.IR.A.sdk_classes import Position
```

### 属性

| 属性  | 类型      | 描述   |
|-----|---------|------|
| `x` | `float` | X轴坐标 |
| `y` | `float` | Y轴坐标 |
| `z` | `float` | Z轴坐标 |
| `a` | `float` | A轴角度 |
| `b` | `float` | B轴角度 |
| `c` | `float` | C轴角度 |

## 3.10 Posture

### 说明

描述机器人形态参数的数据结构

### 导入

```python
from Agilebot.IR.A.sdk_classes import Posture
```

### 属性

| 属性               | 类型      | 描述        |
|------------------|---------|-----------|
| `turnCircle`     | `int[]` | 各关节的回转圈数  |
| `wrist_flip`     | `int`   | 表示手腕翻转状态  |
| `arm_up_down`    | `int`   | 表示手臂的上下状态 |
| `arm_back_front` | `int`   | 表示手臂的前后状态 |
| `arm_left_right` | `int`   | 表示手臂的左右状态 |

## 3.11 BaseCartData

### 说明

描述机器人笛卡尔目标位姿的数据结构

### 导入

```python
from Agilebot.IR.A.sdk_classes import BaseCartData
```

### 属性

| 属性         | 类型                 | 描述       |
|------------|--------------------|----------|
| `position` | [`Position`](#3-9) | 笛卡尔位姿的数据 |
| `posture`  | [`Posture`](#3-10) | 机器人形态参数  |

## 3.12 MotionPose

### 说明

描述机器人点位的结构 坐标数据中，XYZ方向距离数据单位为毫米 （mm），角度数据单位为 度 （°），部分版本角度信息为弧度，详见功能列表返回结果说明。

### 导入

```python
from Agilebot.IR.A.sdk_classes import MotionPose
```

### 属性

| 属性         | 类型                      | 描述                                                                                  |
|------------|-------------------------|-------------------------------------------------------------------------------------|
| `cartData` | [`BaseCartData`](#3-10) | 笛卡尔数据                                                                               |
| `joint`    | [`Joint`](#3-7)         | 关节数据                                                                                |
| `pt`       | [`PoseType`](#3-6)              | 点位类型，默认为 PoseType.JOINT                 |

## 3.13 DHparam

### 说明

机器人DH参数列表

### 导入

```python
from Agilebot.IR.A.sdk_classes import DHparam
```

### 属性

| 属性       | 类型      | 描述      | 默认值  |
|----------|---------|---------|------|
| `id`     | `int`   | DH参数的ID | -1   |
| `d`      | `float` | 关节距离    | -1.0 |
| `a`      | `float` | 杆件长度    | -1.0 |
| `alpha`  | `float` | 杆件扭角    | -1.0 |
| `offset` | `float` | 关节转角    | -1.0 |

## 3.14 Payload

### 说明

机器人负载信息

### 导入

```python
from Agilebot.IR.A.flyshot import Payload
```

### 属性

| 描述       | 字段名         | 类型             | 默认值 |
|----------|-------------|----------------|-----|
| 序号 ID    | `_id`       | `c_int`        |     |
| 是否有效     | `_is_valid` | `c_bool`       |     |
| 负载重量（kg） | `_m_load`   | `c_double`     |     |
| 负载质心 x   | `_lcx_load` | `c_double`     |     |
| 负载质心 y   | `_lcy_load` | `c_double`     |     |
| 负载质心 z   | `_lcz_load` | `c_double`     |     |
| 转动惯量 Ix  | `_Ixx_load` | `c_double`     |     |
| 转动惯量 Iy  | `_Iyy_load` | `c_double`     |     |
| 转动惯量 Iz  | `_Izz_load` | `c_double`     |     |
| 转动惯量     | `_Ixy_load` | `c_double`     | 0   |
| 转动惯量     | `_Ixz_load` | `c_double`     | 0   |
| 转动惯量     | `_Iyz_load` | `c_double`     | 0   |
| 注释       | `_comment`  | `c_char * 256` |     |

## 3.15 ProgramCartData

### 说明

程序点位信息

### 导入

```python
from Agilebot.IR.A.sdk_classes import ProgramCartData
```

### 属性

| 属性         | 类型                      | 描述         |
|------------|-------------------------|------------|
| `baseCart` | [`BaseCartData`](#3-10) | 笛卡尔数据      |
| `uf`       | int                     | 使用的用户坐标系ID |
| `tf`       | int                     | 使用的工具坐标系ID |

## 3.16 ProgramPoseData

### 说明

程序点位信息

### 导入

```python
from Agilebot.IR.A.sdk_classes import ProgramPoseData
```

### 属性

| 属性         | 类型                         | 描述                                                                                   |
|------------|----------------------------|--------------------------------------------------------------------------------------|
| `poseData` | [`ProgramCartData`](#3-15) | 程序点位数据                                                                               |
| `joint`    | [`Joint`](#3-7)            | 关节数据                                                                                 |
| `pt`       | `string`                   | 点位类型，默认为 unknown - joint 表示关节坐标系 - cart 表示笛卡尔坐标系 - unknown 表示未知坐标系类型  |

## 3.17 ProgramPose

### 说明

程序点位信息

### 导入

```python
from Agilebot.IR.A.sdk_classes import ProgramPose
```

### 属性

| 属性         | 类型                         | 描述     |
|------------|----------------------------|--------|
| `poseData` | [`ProgramPoseData`](#3-16) | 程序点位数据 |
| `id`       | int                        | 点位ID   |
| `name`     | `string`                   | 点位名称   |
| `comment`  | `string`                   | 点位注释   |

## 3.18 PoseRegisterData

### 说明

寄存器点类，用于表示和处理机械臂的寄存器点数据。

### 导入

```python
from Agilebot.IR.A.sdk_classes import ProgramPoseData
```

### 属性

| 属性         | 类型                         | 描述                                                                                   |
|------------|----------------------------|--------------------------------------------------------------------------------------|
| `poseData` | [`BaseCartData`](#3-10) | 程序点位数据                                                                               |
| `joint`    | [`Joint`](#3-7)            | 关节数据                                                                                 |
| `pt`       | [`PoseType`](#3-6)              | 点位类型，默认为 PoseType.JOINT                 |

## 3.19 PoseRegister

### 说明

寄存器点类，用于表示和处理机械臂的寄存器点数据。

### 导入

```python
from Agilebot.IR.A.sdk_classes import PoseRegister
```

### 属性

| 属性         | 类型                         | 描述     |
|------------|----------------------------|--------|
| `poseRegisterData` | [`PoseRegisterData`](#3-18) | 程序点位数据 |
| `id`       | `int`                      | 点位ID   |
| `name`     | `string`                   | 点位名称   |
| `comment`  | `string`                   | 点位注释   |

## 3.20 TransformStatusEnum

### 说明

离线轨迹文件转换状态的枚举

### 导入

```python
from Agilebot.IR.A.sdk_types import TransformStatusEnum
```

### 字段

| 名称                  | 枚举值 | 描述        |
|---------------------|-----|-----------|
| TRANSFORM\_START     | 0   | 转换任务开始    |
| TRANSFORM\_RUNNING   | 1   | 转换任务执行中   |
| TRANSFORM\_SUCCESS   | 2   | 转换任务已完成   |
| TRANSFORM\_FAILED    | 3   | 转换任务失败    |
| TRANSFORM\_NOT\_FOUND | 4   | 转换任务没找到   |
| TRANSFORM\_UNKNOWN   | 5   | 未知的转换任务状态 |

## 3.21 HWState

### 说明

机器人状态HWState枚举

### 导入

```python
from Agilebot.IR.A.sdk_types import HWState
```

### 字段

| 名称                       | 枚举值 | 描述           |
|--------------------------|-----|--------------|
| TOPIC\_JOINT              | 0   | 发布机械臂关节状态反馈  |
| TOPIC\_CURRENT\_CARTESIAN  | 1   | 发布TCP当前笛卡尔坐标 |
| TOPIC\_UF                 | 2   | 发布当前用户坐标系信息  |
| TOPIC\_TF                 | 3   | 发布当前工具坐标系信息  |
| TOPIC\_VELOCITY           | 4   | 发布全局速度比率     |
| TOPIC\_RUNNING\_STATUS     | 5   | 发布控制器运行状态    |
| TOPIC\_INTERPRETER\_STATUS | 6   | 发布解释器状态      |
| TOPIC\_ROBOT\_STATUS       | 7   | 发布机器人状态      |
| TOPIC\_CTRL\_STATUS        | 8   | 发布控制器状态      |
| TOPIC\_SERVO\_STATUS       | 9   | 发布伺服控制器状态    |

## 3.22 CoordinateSystemType

### 说明

机器人坐标系相关信息

### 导入

```python
from Agilebot.IR.A.sdk_types import CoordinateSystemType
```

### 字段

| 名称         | 枚举值 | 描述    |
|------------|-----|-------|
| USER\_FRAME | 0   | 用户坐标系 |
| TOOL\_FRAME | 1   | 工具坐标系 |

## 3.23 CoordinateInfo

### 说明

坐标系信息类，用于存储坐标系的相关信息。

### 导入

```python
from Agilebot.IR.A.sdk_classes import CoordinateInfo
```

### 属性

| 属性              | 类型       | 描述    |
|-----------------|----------|-------|
| `coordinate_id` | `int`    | 坐标系ID |
| `name`          | `string` | 坐标系名称 |
| `comment`       | `string` | 坐标系注释 |
| `group_id`      | `int`    | 组ID   |

## 3.24 Translation

### 说明

描述机器人的几何位置和姿态信息。

### 导入

```python
from Agilebot.IR.A.sdk_classes import Translation
```

### 属性

| 属性  | 类型      | 描述     |
|-----|---------|--------|
| `x` | `float` | x轴位置信息 |
| `y` | `float` | y轴位置信息 |
| `z` | `float` | z轴位置信息 |

## 3.25 Rotation

### 说明

描述机器人的姿态信息。

### 导入

```python
from Agilebot.IR.A.sdk_classes import Rotation
```

### 属性

| 属性  | 类型      | 描述       |
|-----|---------|----------|
| `r` | `float` | 绕X轴的旋转角度 |
| `p` | `float` | 绕Y轴的旋转角度 |
| `y` | `float` | 绕Z轴的旋转角度 |

## 3.26 GeometryPose

### 说明

机器人几何位置和姿态信息类，用于表示机器人的几何位置和姿态信息。

### 引用

```python
from Agilebot.IR.A.sdk_classes import GeometryPose
```

### 属性

| 属性                | 类型                        | 描述    |
|-------------------|---------------------------|-------|
| `coordinate_info` | [`CoordinateInfo`](#3-23) | 坐标系信息 |
| `position`        | [`Translation`](#3-24)    | 位置信息  |
| `orientation`     | [`Rotation`](#3-25)       | 姿态信息  |

## 3.27 DragStatus

### 说明

机器人轴拖动状态类

### 导入

```python
from Agilebot.IR.A.sdk_classes import DragStatus
```

### 属性

| 属性                   | 类型                     | 描述             |
|----------------------|------------------------|----------------|
| `cart_status`        | [`CartStatus`](#3-28)  | 笛卡尔坐标系各轴拖动锁定状态 |
| `joint_status`       | [`JointStatus`](#3-29) | 关节轴拖动锁定状态      |
| `is_continuous_drag` | `bool`                 | 持续拖动的标志        |

## 3.28 CartStatus

### 说明

笛卡尔状态类，用于表示笛卡尔坐标系的状态。

### 导入

```python
from Agilebot.IR.A.sdk_classes import CartStatus
```

### 属性

| 属性  | 类型     | 描述   |
|-----|--------|------|
| `x` | `bool` | X轴状态 |
| `y` | `bool` | Y轴状态 |
| `z` | `bool` | Z轴状态 |
| `a` | `bool` | A轴状态 |
| `b` | `bool` | B轴状态 |
| `c` | `bool` | C轴状态 |

## 3.29 JointStatus

### 说明

关节状态类，用于表示机械臂各关节的状态。所有关节的状态默认为True（可用）。

### 导入

```python
from Agilebot.IR.A.sdk_classes import JointStatus
```

### 属性

| 属性   | 类型     | 描述    |
|------|--------|-------|
| `j1` | `bool` | J1轴状态 |
| `j2` | `bool` | J2轴状态 |
| `j3` | `bool` | J3轴状态 |
| `j4` | `bool` | J4轴状态 |
| `j5` | `bool` | J5轴状态 |
| `j6` | `bool` | J6轴状态 |
| `j7` | `bool` | J7轴状态 |
| `j8` | `bool` | J8轴状态 |
| `j9` | `bool` | J9轴状态 |

## 3.30 ModbusChannel

### 说明

Modbus通道类型

### 导入

```python
from Agilebot.IR.A.sdk_types import ModbusChannel
```

### 属性

| 名称       | 枚举值   | 描述                                      |
|------------|--------|-------------------------------------------|
| CONTROLLER\_TCP\_TO\_485  | 2    | TCP2RS485模块通道。   |
| WRIST\_485\_0   | 3    | 手腕AI通道。   |
| WRIST\_485\_1    | 4    | 手腕DO通道。     |
| CONTROLLER\_485     | 5    | 控制柜485通道。     |

## 3.31 PayloadIdentifyState

### 说明

负载测定状态。

### 导入

```python
from Agilebot.IR.A.sdk_types import PayloadIdentifyState
```

### 属性

| 名称                  | 枚举值 | 描述        |
|---------------------|-----|-----------|
| PAYLOAD\_CHECK\_INIT     | 0   | 负载测定检查初始化中    |
| PAYLOAD\_CHECK\_RUNNING   | 1   | 负载测定检查运行中   |
| PAYLOAD\_CHECK\_SUCCESS   | 2   | 负载测定检查成功   |
| PAYLOAD\_CHECK\_FAILED    | 3   | 负载测定检查失败    |
| PAYLOAD\_IDENTIFY\_INIT   | 4   | 负载测定初始化   |
| PAYLOAD\_IDENTIFY\_RUNNING   | 5   | 负载测定运行中 |
| PAYLOAD\_IDENTIFY\_SUCCESS   | 6   | 负载测定成功 |
| PAYLOAD\_IDENTIFY\_FAILED   | 7   | 负载测定失败 |

## 3.32 MoveMode

### 说明

Modbus通道类型

### 导入

```python
from Agilebot.IR.A.jogging import MoveMode
```

### 属性

| 名称       | 枚举值   | 描述                                      |
|------------|--------|-------------------------------------------|
| Continuous  | 0    | 增量运动   |
| Stepping   | 1    | 连续运动   |

## 3.33 SignalType

### 说明

`SignalType` 是一个枚举类，用于区分不同类型的输入输出信号。它涵盖了数字信号、专用信号、手臂信号、组信号、模拟信号等多种类型，帮助在机器人控制系统中准确识别和管理不同类型的信号。

### 导入

```python
from Agilebot.IR.Types import SignalType
```

### 枚举值

| 名称       | 枚举值   | 描述                                      |
|------------|----------|-------------------------------------------|
| `DI`       | 1        | 数字输入信号（Digital Input）             |
| `DO`       | 2        | 数字输出信号（Digital Output）            |
| `UI`       | 3        | 专用输入信号（User Input）                |
| `UO`       | 4        | 专用输出信号（User Output）               |
| `RI`       | 5        | 手臂输入信号（Robot Input）               |
| `RO`       | 6        | 手臂输出信号（Robot Output）              |
| `GI`       | 7        | 组输入信号（Group Input）                 |
| `GO`       | 8        | 组输出信号（Group Output）                |
| `TAI`      | 9        | 手腕模拟输入信号（Tool Analog Input）     |
| `TDI`      | 10       | 手腕数字输入信号（Tool Digital Input）    |
| `TDO`      | 11       | 手腕数字输出信号（Tool Digital Output）   |
| `AI`       | 12       | 模拟输入信号（Analog Input）              |
| `AO`       | 13       | 模拟输出信号（Analog Output）             |

### 3.33.1 SignalValue

#### 说明

`SignalValue` 类用于定义信号的开关值。它通过两个常量 `OFF` 和 `ON` 来表示信号的关闭和开启状态。此类在机器人控制系统中用于控制和读取信号的状态。

### 导入

```python
from Agilebot.IR.Types import SignalValue
```

### 属性

| 名称       | 值   | 描述                                      |
|------------|------|-------------------------------------------|
| `OFF`      | 0    | 信号关闭                                  |
| `ON`       | 1    | 信号开启                                  |
