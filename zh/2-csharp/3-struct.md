---
url: /zh/2-csharp/3-struct.md
---
# 3 数据结构

## 3.1 StatusCode

### 说明

接口返回状态码

### 导入

```c#
using Agilebot.IR;
```

### 字段

| **名称**                                 | **枚举值** | **描述**                         |
|----------------------------------------|---------|--------------------------------|
| `OK`                                   | 0       | 执行成功                        |
| `INCOMPATIBLE_VERSION`                 | -1      | 版本不兼容                       |
| `TIMEOUT`                              | -3      | 连接超时                        |
| `INTERFACE_NOT_IMPLEMENTED`            | -4      | 接口未实现                       |
| `INDEX_OUT_OF_RANGE`                   | -5      | 索引越界                        |
| `UNSUPPORTED_FILETYPE`                 | -6      | 不支持的文件类型                |
| `UNSUPPORTED_PARAMETER`                | -7      | 不支持的机器人参数               |
| `UNSUPPORTED_SIGNALTYPE`               | -8      | 不支持的IO信号类型               |
| `PROGRAM_NOT_FOUND`                    | -9      | 找不到程序                       |
| `PROGRAM_POSE_NOT_FOUND`               | -10     | 找不到程序位姿信息               |
| `WRITE_PROGRAM_FAILED`                 | -11     | 更新程序位姿信息失败             |
| `GET_ALARM_CODE_FAILED`                | -12     | 访问报警服务获取报警码失败        |
| `WRONG_POSITION_INFO`                  | -13     | 控制器返回错误的点位信息          |
| `UNSUPPORTED_TRA_TYPE`                 | -14     | 不支持的运动类型                 |
| `FILE_NOT_FOUND`                       | -15     | 文件或文件夹未找到               |
| `FILE_ALREADY_EXIST`                   | -16     | 文件已存在                       |
| `GET_ALARM_DESC_FAILED`                | -17     | 根据报警码获取报警信息失败        |
| `RESET_ALARM_ERRORS_FAILED`            | -18     | 重置报警信息失败                 |
| `GET_ALL_ALARMS_FAILED`                | -19     | 获取所有报警信息失败              |
| `WRONG_DATA_FORMAT`                    | -20     | 接收的数据格式有误               |
| `CONNECT_FAILED`                       | -21     | 初始化连接失败，请检查ip地址或控制柜服务 |
| `POSE_INDEX_DUPLICATED`                | -23     | 位姿序号重复                     |
| `CONTROLLER_ERROR`                     | -254    | 控制器错误，请联系开发人员        |
| `OTHER_REASON`                         | -255    | 其他原因                         |

## 3.2 RobotState

### 说明

机器人运行状态

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| **名称**                   | **枚举值** | **描述**          |
|--------------------------|---------|-----------------|
| `WRONG_DATA`             | -1      | 未知状态            |
| `ROBOT_IDLE`             | 0       | 机器人空闲           |
| `ROBOT_RUNNING`          | 1       | 机器人运行中          |
| `ROBOT_TEACHING`         | 2       | 机器人示教中          |
| `ROBOT_IDLE_TO_RUNNING`  | 101     | 机器人中间状态 空闲转换为运行 |
| `ROBOT_IDLE_TO_TEACHING` | 102     | 机器人中间状态 空闲转换为示教 |
| `ROBOT_RUNNING_TO_IDLE`  | 103     | 机器人中间状态 运行转换为空闲 |
| `ROBOT_TEACHING_TO_IDLE` | 104     | 机器人中间状态 示教转换为空闲 |

## 3.3 CtrlState

### 说明

控制器运行状态

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| 名称                         | 枚举值 | 描述              |
|----------------------------|-----|-----------------|
| `WRONG_DATA`               | -1  | 未知的控制器状态        |
| `CTRL_INIT`                | 0   | 控制器初始化          |
| `CTRL_ENGAGED`             | 1   | 控制器使能           |
| `CTRL_ESTOP`               | 2   | 控制器急停           |
| `CTRL_TERMINATED`          | 3   | 控制器中止           |
| `CTRL_ANY_TO_ESTOP`        | 101 | 控制器中间状态 其他转换为急停 |
| `CTRL_ESTOP_TO_ENGAGED`    | 102 | 控制器中间状态 急停到使能   |
| `CTRL_ESTOP_TO_TERMINATED` | 103 | 控制器中间状态 急停到中止   |

## 3.4 ServoState

### 说明

伺服控制器状态

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| 名称                 | 枚举值 | 描述         |
|--------------------|-----|------------|
| `WRONG_DATA`       | -1  | 未知的伺服控制器状态 |
| `SERVO_IDLE`       | 1   | 伺服控制器空闲    |
| `SERVO_RUNNING`    | 2   | 伺服控制器运行中   |
| `SERVO_DISABLE`    | 3   | 伺服控制器关闭    |
| `SERVO_WAIT_READY` | 4   | 伺服控制器等待就绪  |
| `SERVO_WAIT_DOWN`  | 5   | 伺服控制器等待关闭  |
| `SERVO_INIT`       | 10  | 伺服控制器初始化   |

## 3.5 TransformStatusEnum

### 说明

离线轨迹文件转换状态的枚举

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| 名称                  | 枚举值 | 描述        |
|---------------------|-----|-----------|
| `TRANSFORM_START`     | 0   | 转换任务开始    |
| `TRANSFORM_RUNNING`   | 1   | 转换任务执行中   |
| `TRANSFORM_SUCCESS`   | 2   | 转换任务已完成   |
| `TRANSFORM_FAILED`    | 3   | 转换任务失败    |
| `TRANSFORM_NOT_FOUND` | 4   | 转换任务没找到   |
| `TRANSFORM_UNKNOWN`   | -1  | 未知的转换任务状态 |

以下是为 `PayloadInfo`、`MassCenter` 和 `InertiaMoment` 类生成的详细说明文档：

***

## 3.6 PayloadInfo

### 说明

`PayloadInfo` 类用于存储机器人的负载信息，包括负载编号、重量、质心和惯性矩等参数。这些信息对于机器人在负载条件下的运动学和动力学分析至关重要，尤其是在进行路径规划和力矩计算时。

### 导入

```c#
using Agilebot.IR.Motion;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `Id` | `uint` | 负载编号，用于唯一标识不同的负载配置 |
| `Comment` | `string` | 注释，用于描述负载的额外信息 |
| `Weight` | `double` | 负载的重量（单位：千克） |
| `MassCenter` | [`MassCenter`](#3-6-1) | 负载的质心位置（X、Y、Z 坐标） |
| `InertiaMoment` | [`InertiaMoment`](#3-6-2) | 负载的惯性矩（LX、LY、LZ） |

### 示例

```c#
PayloadInfo payload = new PayloadInfo
{
    Id = 1,
    Comment = "Sample Payload",
    Weight = 5.0,
    MassCenter = new MassCenter { X = 10.0, Y = 20.0, Z = 30.0 },
    InertiaMoment = new InertiaMoment { LX = 0.1, LY = 0.2, LZ = 0.3 }
};

```

### 3.6.1 MassCenter

#### 说明

`MassCenter` 类用于表示负载的质心位置，包含 X、Y 和 Z 三个坐标轴的值。质心位置是负载在空间中的几何中心，对于机器人运动控制和力矩计算非常重要。

#### 导入

```c#
using Agilebot.IR.Motion;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `X` | `double` | 质心的 X 坐标（单位：毫米） |
| `Y` | `double` | 质心的 Y 坐标（单位：毫米） |
| `Z` | `double` | 质心的 Z 坐标（单位：毫米） |

### 3.6.2 InertiaMoment

#### 说明

`InertiaMoment` 类用于表示负载的惯性矩，包含 LX、LY 和 LZ 三个方向的值。惯性矩是负载在旋转运动中抵抗变化的能力，对于机器人动力学分析和控制非常重要。

#### 导入

```c#
using Agilebot.IR.Motion;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `LX` | `double` | 惯性矩的 X 分量（单位：千克·毫米²） |
| `LY` | `double` | 惯性矩的 Y 分量（单位：千克·毫米²） |
| `LZ` | `double` | 惯性矩的 Z 分量（单位：千克·毫米²） |

## 3.7 TransformState

### 说明

离线轨迹文件转换状态的枚举

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| 枚举值                   | 值  | 描述        |
| --------------------- | -- | --------- |
| `TRANSFORM_START`     | 0  | 转换任务开始    |
| `TRANSFORM_RUNNING`   | 1  | 转换任务执行中   |
| `TRANSFORM_SUCCESS`   | 2  | 转换任务已完成   |
| `TRANSFORM_FAILED`    | 3  | 转换任务失败    |
| `TRANSFORM_NOT_FOUND` | 4  | 转换任务未找到   |
| `TRANSFORM_UNKNOWN`   | -1 | 数据错误，未知状态 |

## 3.8 TCSType

### 说明

TCS坐标系类型

### 导入

```c#
using Agilebot.IR.Types;
```

### 字段

| 名称               | 枚举值 | 描述             |
|-------------------|-----|----------------|
| `WRONG_TYPE`      | -1  | 错误类型       |
| `JOINT`           | 0   | 关节空间       |
| `BASE`            | 1   | 基坐标系       |
| `WORLD`           | 2   | 世界坐标系     |
| `USER`            | 3   | 用户坐标系     |
| `TOOL`            | 4   | 工具坐标系     |
| `RTCP_USER`       | 5   | RTCP用户坐标系 |
| `RTCP_TOOL`       | 6   | RTCP工具坐标系 |

## 3.9 MotionPose

### 说明

描述机器人点位的结构 坐标数据中，XYZ方向距离数据单位为毫米 （mm），角度数据单位为 度 （°），部分版本角度信息为弧度，详见功能列表返回结果说明。

### 导入

```c#
using Agilebot.IR.Motion;
```

### 属性

| 属性       | 类型                    | 描述                                                         |
| ---------- | ----------------------- | ------------------------------------------------------------ |
| `CartData` | [`BaseCartData`](#3-10) | 笛卡尔数据      |
| `Joint`    | [`Joint`](#3-11)         | 关节数据       |
| `Pt`       | [`PoseType`](#3-12)    | 点位类型，默认为 Unknown |

### 示例

```c#
MotionPose motionPose = new MotionPose();
motionPose.Pt = PoseType.Cart;
motionPose.CartData.Position = new Position{
    X  = 300,
    Y = 300,
    Z = 300,
    A = 0,
    B = 0,
    C = 0
};
motionPose.CartData.Posture = new Posture{ 
    WristFlip = 1,
    ArmUpDown = 1,
    ArmBackFront = 1,
    ArmLeftRight = 1,
    TurnCircle = new List<int>(9){0,0,0,0,0,0,0,0,0}
};

MotionPose motionPose2 = new MotionPose();
motionPose2.Pt = PoseType.Joint;
motionPose2.Joint = new Joint{
    J1 = 0,
    J2 = 0,
    J3 = 60,
    J4 = 60,
    J5 = 0,
    J6 = 0
};
```

## 3.10 BaseCartData

### 说明

描述机器人在笛卡尔坐标系中的空间位置和姿态信息。其中，空间坐标使用毫米（mm）为单位，姿态信息包括腕部、臂部的姿态以及各个轴的回转数。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性       | 类型                    | 描述                                                         |
| ---------- | ----------------------- | ------------------------------------------------------------ |
| `Position` | [`Position`](#3-10-1)    | 机器人的空间坐标（X, Y, Z, A, B, C）                         |
| `Posture`  | [`Posture`](#3-10-2)     | 机器人的姿态信息（腕部、臂部姿态及轴的回转数）                |

### 示例

```c#
BaseCartData cartData = new BaseCartData();
cartData.Position.X = 100.0;
cartData.Position.Y = 200.0;
cartData.Position.Z = 300.0;
cartData.Posture.ArmUpDown = 1;
cartData.Posture.ArmBackFront = -1;
Console.WriteLine(cartData.ToString());
```

***

### 3.10.1 Position

#### 说明

描述机器人操作点的笛卡尔坐标系空间位置及旋转角度坐标。坐标数据中，X、Y、Z 方向的距离单位为毫米（mm），A、B、C 方向的角度单位为度（°）。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性       | 类型    | 描述                                                         |
| ---------- | ------- | ------------------------------------------------------------ |
| `X`        | `double`| 笛卡尔坐标系 X 方向的距离（单位：毫米）                      |
| `Y`        | `double`| 笛卡尔坐标系 Y 方向的距离（单位：毫米）                      |
| `Z`        | `double`| 笛卡尔坐标系 Z 方向的距离（单位：毫米）                      |
| `A`        | `double`| 笛卡尔坐标系 A 方向的角度（单位：度）                        |
| `B`        | `double`| 笛卡尔坐标系 B 方向的角度（单位：度）                        |
| `C`        | `double`| 笛卡尔坐标系 C 方向的角度（单位：度）                        |

#### 示例

```c#
Position position = new Position();
position.X = 100.0;
position.Y = 200.0;
position.Z = 300.0;
position.A = 45.0;
position.B = 30.0;
position.C = 60.0;
Console.WriteLine(position.ToString());
```

***

### 3.10.2 Posture

#### 说明

描述机器人的姿态信息，包括腕部、臂部的姿态以及各个轴的回转数。姿态信息用于定义机器人在空间中的具体姿态。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性           | 类型          | 描述                                                         |
| -------------- | ------------- | ------------------------------------------------------------ |
| `TurnCircle`   | `List<int>`   | 各个轴的回转数，取值范围为 -1、0、1                           |
| `WristFlip`    | `int`         | 腕部翻转姿态，取值范围为 -1、0、1                             |
| `ArmUpDown`    | `int`         | 臂部上下姿态，取值范围为 -1、0、1                             |
| `ArmBackFront` | `int`         | 臂部前后姿态，取值范围为 -1、0、1                             |
| `ArmLeftRight` | `int`         | 臂部左右姿态，取值范围为 -1、0、1                             |

#### 示例

```c#
Posture posture = new Posture();
posture.TurnCircle = new List<int>(9){0,0,0,0,0,0,0,0,0}
posture.WristFlip = 1;
posture.ArmUpDown = 1;
posture.ArmBackFront = -1;
posture.ArmLeftRight = 1;
Console.WriteLine(posture.ToString());
```

以下是为 `Joint` 类生成的说明文档：

***

## 3.11 Joint

### 说明

描述机器人各个关节的角度数据。每个关节的角度值用于定义机器人在关节空间中的具体位置。角度单位通常为度（°），但具体单位需根据实际机器人系统确认。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性   | 类型    | 描述                     |
| ------ | ------- | ------------------------ |
| `J1`   | `double`| 机器人一轴的关节角度     |
| `J2`   | `double`| 机器人二轴的关节角度     |
| `J3`   | `double`| 机器人三轴的关节角度     |
| `J4`   | `double`| 机器人四轴的关节角度     |
| `J5`   | `double`| 机器人五轴的关节角度     |
| `J6`   | `double`| 机器人六轴的关节角度     |
| `J7`   | `double`| 机器人七轴的关节角度     |
| `J8`   | `double`| 机器人八轴的关节角度     |
| `J9`   | `double`| 机器人九轴的关节角度     |

### 示例

```c#
Joint joint = new Joint();
joint.J1 = 45.0;
joint.J2 = 30.0;
joint.J3 = 60.0;
joint.J4 = 90.0;
joint.J5 = 120.0;
joint.J6 = 135.0;
joint.J7 = 150.0;
joint.J8 = 180.0;
joint.J9 = 225.0;
Console.WriteLine(joint.ToString());
```

### 注意事项

* 关节角度的单位通常为度（°），但某些机器人系统可能使用弧度（rad）。请根据具体机器人系统的文档确认单位。
* 关节角度的取值范围通常由机器人硬件限制，超出范围可能导致错误或损坏设备。

以下是为 `PoseType` 枚举生成的说明文档：

***

## 3.12 PoseType

### 说明

定义了机器人位姿数据的类型，用于区分数据是关节角度、笛卡尔空间坐标还是未知类型。该枚举用于标识机器人位姿数据的格式，以便在程序中正确处理不同类型的数据。

### 导入

```c#
using Agilebot.IR.Types;
```

### 枚举值

| 枚举值    | 描述                             |
|-----------|----------------------------------|
| `Unknown` | 未知类型，表示位姿数据类型未定义 |
| `Joint`   | 关节角度数据类型，表示数据为关节角度 |
| `Cart`    | 笛卡尔空间坐标数据类型，表示数据为笛卡尔坐标 |

以下是为 `DHparam` 类生成的说明文档：

***

## 3.13 DHparam

### 说明

`DHparam` 类用于描述机器人连杆的参数，基于 [Denavit-Hartenberg 参数](https://en.wikipedia.org/wiki/Denavit%E2%80%93Hartenberg_parameters)（D-H 参数）。这些参数用于定义机器人关节之间的几何关系，是机器人运动学和动力学分析的基础。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性       | 类型      | 描述                                                         |
|------------|-----------|--------------------------------------------------------------|
| `id`       | `uint`    | 杆件的唯一标识符，用于区分不同的连杆                         |
| `a`        | `double`  | 杆件长度，表示相邻关节的轴向距离（单位：毫米）               |
| `alpha`    | `double`  | 杆件扭角，表示相邻关节轴之间的夹角（单位：度或弧度）         |
| `d`        | `double`  | 关节距离，表示沿当前关节轴到下一个关节的距离（单位：毫米）   |
| `offset`   | `double`  | 关节转角偏移量，表示关节的初始角度偏移（单位：度或弧度）      |

### 构造函数

```c#
public DHparam(uint id, double d, double a, double alpha, double offset)
```

### 注意事项

* **单位一致性**：`a` 和 `d` 的单位应保持一致（通常为毫米），而 `alpha` 和 `offset` 的单位也应保持一致（通常为度或弧度）。
* **角度单位**：在某些机器人系统中，角度单位可能为弧度而非度。请根据实际需求确认并统一单位。
* **D-H 参数的定义**：D-H 参数的定义依赖于具体的机器人模型和坐标系约定。在使用 `DHparam` 类时，确保参数的定义与机器人的实际几何结构一致。

以下是为 `CartStatus`、`JointStatus` 和 `DragStatus` 类生成的详细说明文档：

***

## 3.14 CartStatus

### 说明

`CartStatus` 类用于表示笛卡尔坐标系中各轴的状态。每个轴的状态用布尔值表示，`true` 表示轴可用，`false` 表示轴不可用。此状态类通常用于机器人运动控制中，以判断某个轴是否可以正常工作。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `X`  | `bool` | X 方向状态，默认为 `true`（可用） |
| `Y`  | `bool` | Y 方向状态，默认为 `true`（可用） |
| `Z`  | `bool` | Z 方向状态，默认为 `true`（可用） |
| `A`  | `bool` | A 方向状态，默认为 `true`（可用） |
| `B`  | `bool` | B 方向状态，默认为 `true`（可用） |
| `C`  | `bool` | C 方向状态，默认为 `true`（可用） |

***

## 3.15 JointStatus

### 说明

`JointStatus` 类用于表示机械臂各关节的状态。每个关节的状态用布尔值表示，`true` 表示关节可用，`false` 表示关节不可用。此状态类通常用于机器人运动控制中，以判断某个关节是否可以正常工作。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `J1` | `bool` | 关节1状态，默认为 `true`（可用） |
| `J2` | `bool` | 关节2状态，默认为 `true`（可用） |
| `J3` | `bool` | 关节3状态，默认为 `true`（可用） |
| `J4` | `bool` | 关节4状态，默认为 `true`（可用） |
| `J5` | `bool` | 关节5状态，默认为 `true`（可用） |
| `J6` | `bool` | 关节6状态，默认为 `true`（可用） |
| `J7` | `bool` | 关节7状态，默认为 `true`（可用） |
| `J8` | `bool` | 关节8状态，默认为 `true`（可用） |
| `J9` | `bool` | 关节9状态，默认为 `true`（可用） |

***

## 3.16 DragStatus

### 说明

`DragStatus` 类用于表示机械臂的拖动状态，包含笛卡尔坐标系状态和关节状态。此外，还包含一个标志位 `IsContinuousDrag`，用于表示是否处于连续拖动模式。此状态类通常用于机器人拖动控制中，以判断当前的拖动模式和各轴/关节的状态。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `CartStatus` | [`CartStatus`](#3-14) | 笛卡尔坐标系状态 |
| `JointStatus` | [`JointStatus`](#3-15) | 关节状态 |
| `IsContinuousDrag` | `bool` | 是否处于连续拖动模式，默认为 `false` |

### 构造函数

```c#
public DragStatus()
```

* 初始化 `CartStatus` 和 `JointStatus`，并设置 `IsContinuousDrag` 为 `false`。

### 示例

```c#
DragStatus dragStatus = new DragStatus();
dragStatus.CartStatus.X = false; // X轴不可用
dragStatus.JointStatus.J3 = false; // 关节3不可用
dragStatus.IsContinuousDrag = true; // 设置为连续拖动模式
Console.WriteLine($"X轴状态: {dragStatus.CartStatus.X}, 关节3状态: {dragStatus.JointStatus.J3}, 是否连续拖动: {dragStatus.IsContinuousDrag}");
```

## 3.17 ProgramPose

### 说明

`ProgramPose` 类用于表示程序中的一个位姿（姿态），可以是关节坐标或笛卡尔坐标。该类包含位姿的唯一标识符、数据（关节或笛卡尔坐标信息）、名称和注释。通过此类，可以方便地管理和操作机器人程序中的位姿信息。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `Id` | `int` | 位姿的唯一标识符 |
| `PoseData` | [`ProgramPoseData`](#3-17-1) | 位姿的数据，包括关节或笛卡尔坐标信息 |
| `Name` | `string` | 位姿的名称 |
| `Comment` | `string` | 位姿的注释 |

### 构造函数

```c#
public ProgramPose()
```

* 初始化 `Id`、`PoseData`、`Name` 和 `Comment`。

### 示例

```c#
ProgramPose programPose = new ProgramPose();
programPose.Id = 1; // 设置位姿的唯一标识符
programPose.PoseData = new ProgramPoseData(); // 创建位姿数据
programPose.Name = "Pose1"; // 设置位姿名称
programPose.Comment = "这是一个示例位姿"; // 设置位姿注释
Console.WriteLine($"位姿ID: {programPose.Id}, 名称: {programPose.Name}, 注释: {programPose.Comment}");
```

### 3.17.1 ProgramPoseData

#### 说明

`ProgramPoseData` 类用于表示程序中的位姿数据，包含笛卡尔空间坐标和姿态信息、关节角度信息以及位姿类型。通过此类，可以方便地存储和管理位姿的具体数据。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `CartData` | [`ProgramCartData`](#3-17-2) | 笛卡尔数据      |
| `Joint`    | [`Joint`](#3-11)         | 关节数据       |
| `Pt`       | [`PoseType`](#3-12)    | 点位类型，默认为 Unknown |

### 3.17.2 ProgramCartData

#### 说明

`ProgramCartData` 类用于表示程序的笛卡尔坐标系数据。它通过引用 `BaseCartData` 类来包含空间坐标和姿态信息，并通过 `Uf` 和 `Tf` 的值来确定采用的坐标系类型。`Uf` 表示用户坐标系（User Frame），`Tf` 表示工具坐标系（Tool Frame）。如果 `Uf` 和 `Tf` 的值为 `-1`，则表示使用系统的默认坐标系。此类在机器人编程中用于定义和管理笛卡尔空间中的位姿信息。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `BaseCart` | [`BaseCartData`](#3-10) | 机器人的笛卡尔点位和姿态信息 |
| `Uf` | `int` | 用户坐标系（User Frame），`-1` 表示使用系统的坐标系 |
| `Tf` | `int` | 工具坐标系（Tool Frame），`-1` 表示使用系统的坐标系 |

## 3.18 FileType

### 说明

`FileType` 枚举用于定义文件上传时允许的文件类型。它通过不同的枚举值来区分机器人程序文件的来源和格式。此枚举在机器人编程环境中用于文件管理、上传和程序解析等场景，帮助系统正确识别和处理不同类型的程序文件。

### 导入

```c#
using Agilebot.IR.Types;
```

### 枚举值

| 枚举值 | 描述 |
|--------|------|
| `UserProgram` | 用户通过点选生成的程序文件，每个程序包含 `.xml` 和 `.json` 两个文件。 |
| `BlockProgram` | 用户通过积木块生成的程序文件，每个程序包含 `.block`、`.xml` 和 `.json` 文件。 |
| `TrajectoryProgram` | 离线轨迹程序文件，通常用于离线编程生成的路径规划文件。 |

## 3.19 SignalType

### 说明

`SignalType` 枚举用于定义机器人系统中支持的信号类型。它通过不同的枚举值来区分各种数字信号和模拟信号的用途和来源。此枚举在机器人控制系统中用于信号配置、信号处理和逻辑判断等场景，帮助系统准确识别和管理不同类型的信号。

### 导入

```c#
using Agilebot.IR.Types;
```

### 枚举值

| 枚举值 | 描述 |
|--------|------|
| `DI` | 数字信号输入（Digital Input），用于接收外部数字信号。 |
| `DO` | 数字信号输出（Digital Output），用于控制外部设备或执行器。 |
| `RI` | 机器人手臂数字信号输入（Robot Input），用于接收机器人手腕部分的数字信号。 |
| `RO` | 机器人手臂数字信号输出（Robot Output），用于控制机器人手腕部分的执行器。 |
| `UI` | 用户数字信号输入（User Input），用于接收用户自定义的数字信号。 |
| `UO` | 用户数字信号输出（User Output），用于输出用户自定义的数字信号。 |
| `TDI` | 工具数字信号输入（Tool Digital Input），用于接收工具端的数字信号。 |
| `TDO` | 工具数字信号输出（Tool Digital Output），用于控制工具端的执行器。 |
| `GI` | 组输入（Group Input），用于接收一组数字信号的组合输入。 |
| `GO` | 组输出（Group Output），用于输出一组数字信号的组合输出。 |
| `AI` | 模拟输入（Analog Input），用于接收连续变化的模拟信号。 |
| `AO` | 模拟输出（Analog Output），用于输出连续变化的模拟信号。 |
| `TAI` | 手腕模拟输入（Tool Analog Input），用于接收工具端的模拟信号。 |

## 3.20 PoseRegister

### 说明

`PoseRegister` 类用于表示PR寄存器中的位姿（姿态），可以是关节坐标或笛卡尔坐标。该类包含位姿的唯一标识符、数据（关节或笛卡尔坐标信息）、名称和注释。通过此类，可以方便地管理和操作机器人程序中的位姿信息。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `Id` | `int` | 位姿的唯一标识符 |
| `PoseData` | [`PoseRegisterData`](#3-20-1) | 位姿的数据，包括关节或笛卡尔坐标信息 |
| `Name` | `string` | 位姿的名称 |
| `Comment` | `string` | 位姿的注释 |

### 构造函数

```c#
public PoseRegister()
```

* 初始化 `Id`、`PoseData`、`Name` 和 `Comment`。

### 示例

```c#
PoseRegister pose = new PoseRegister();
pose.Id = 1; // 设置位姿的唯一标识符
pose.PoseData = new PoseRegisterData(); // 创建位姿数据
pose.Name = "Pose1"; // 设置位姿名称
pose.Comment = "这是一个示例位姿"; // 设置位姿注释
Console.WriteLine($"位姿ID: {pose.Id}, 名称: {pose.Name}, 注释: {pose.Comment}");
```

### 3.20.1 PoseRegisterData

#### 说明

`PoseRegisterData` 类用于表示PR寄存器中的位姿数据，包含笛卡尔空间坐标和姿态信息、关节角度信息以及位姿类型。通过此类，可以方便地存储和管理位姿的具体数据。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `CartData` | [`BaseCartData`](#3-10) | 笛卡尔数据      |
| `Joint`    | [`Joint`](#3-11)         | 关节数据       |
| `Pt`       | [`PoseType`](#3-12)    | 点位类型，默认为 Unknown |

## 3.22 Coordinate

### 说明

`Coordinate` 类用于表示机器人系统中的一个坐标系。它包含了坐标系的基本信息，如唯一标识符（ID）、名称、备注、运动组编号以及具体的位姿数据。此类在机器人编程和控制系统中用于定义和管理坐标系的具体位置和姿态信息，便于在程序中进行运动规划和路径控制。

### 导入

```c#
using Agilebot.IR.Types;
```

### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `Id` | `int` | 坐标系的唯一标识符。 |
| `Name` | `string` | 坐标系的名称，用于标识和描述坐标系。 |
| `Comment` | `string` | 坐标系的备注信息，用于进一步说明坐标系的用途或特点。 |
| `GroupId` | `int` | 坐标系所属的运动组编号，用于分类管理坐标系。 |
| `Data` | `Position` | 坐标系的具体位姿数据，包含位置和姿态信息。 |

### 示例

```c#
// 创建一个 Coordinate 实例
Coordinate coordinate = new Coordinate
{
    Id = 1, // 设置唯一标识符
    Name = "UserCoordinate1", // 设置名称
    Comment = "这是一个用户自定义坐标系", // 设置备注
    GroupId = 1, // 设置运动组编号
    Data = new Position { X = 100, Y = 200, Z = 300, A = 45, B = 30, C = 60 } // 设置位姿数据
};
```

### 3.22.1 CoordinateType

#### 说明

`CoordinateType` 枚举用于定义坐标系的类型。它通过不同的枚举值来区分用户坐标系和工具坐标系。此枚举在机器人编程和控制系统中用于明确指定坐标系的用途，帮助系统正确处理坐标系相关的操作。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 枚举值

| 枚举值 | 描述 |
|--------|------|
| `UserCoordinate` | 用户坐标系，用于定义用户自定义的坐标系。 |
| `ToolCoordinate` | 工具坐标系，用于定义工具（如末端执行器）的坐标系。 |

### 3.22.2 CoordSummary

#### 说明

`CoordSummary` 类用于表示坐标系的概要信息。它包含坐标系的类型、唯一标识符、名称、注释和组ID等信息。此类在机器人编程环境中用于管理和存储坐标系的元数据，便于在程序中快速访问和操作坐标系。

#### 导入

```c#
using Agilebot.IR.Types;
```

#### 属性

| 属性 | 类型 | 描述 |
|------|------|------|
| `Type` | `CoordinateType` | 坐标系类型，可以是用户坐标系或工具坐标系。 |
| `Id` | `int` | 坐标系的唯一标识符。 |
| `Name` | `string` | 坐标系的名称。 |
| `Comment` | `string` | 坐标系的注释，用于描述坐标系的用途或特点。 |
| `GroupId` | `int` | 坐标系所属的组ID，用于分类管理坐标系。 |

### 示例

```c#
// 创建一个 CoordSummary 实例
CoordSummary coordSummary = new CoordSummary
{
    Type = CoordinateType.UserCoordinate, // 设置为用户坐标系
    Id = 1, // 设置唯一标识符
    Name = "UserCoord1", // 设置名称
    Comment = "这是一个用户自定义坐标系", // 设置注释
    GroupId = 0 // 设置组ID
};
```
