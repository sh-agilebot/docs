---
url: /2-csharp/4-methods.md
---

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

[#3.20.1]: ../3-struct/#3.20.1

[#3.21]: ../3-struct/#3.21

[#3.22]: ../3-struct/#3.22

[#3.22.1]: ../3-struct/#3.22.1

# 4 方法与示例

## 4.1 系统基础操作

| 方法名  | Arm( string `controllerIP` )             |
| ---- | ------------------------------------- |
| 描述   | 根据控制柜IP连接机械臂                          |
| 请求参数 | `controllerIP`: string 控制柜IP地址  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果    |

### 4.1.1 连接机器人

| 方法名  | **Connect**()             |
| ---- | ------------------------------------- |
| 描述   | 根据控制柜IP连接机械臂                          |
| 请求参数 | 无参数  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果    |

### 4.1.2 判断与机械臂的连接是否有效

| 方法名  | **IsConnect**()                        |
| ---- | -------------------------------------- |
| 描述   | 判断与机械臂的连接是否有效                |
| 请求参数 | 无参数          |
| 返回值   | bool: 连接状态，true: 连接有效，false: 连接失效    |

### 4.1.3 与机器人断开连接

| 方法名  | **Disconnect**() |
| ---- | ---------------- |
| 描述   | 断开和机器人的连接        |
| 请求参数 | 无参数              |
| 返回值   | [StatusCode][#3.1]: 函数执行结果    |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();
        if (code == StatusCode.OK){
            Console.WriteLine("Connected successfully.");
        }

        // 检查连接状态
        var state = controller.IsConnect();
        Console.WriteLine("Connected: " + state);

        // 关闭连接
        code = controller.Disconnect();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Disconnected successfully.");
        }
    }
}
```

### 4.1.4 获取当前机器人型号

| 方法名  | **GetArmModelInfo**()      |
| ---- | -------------------------- |
| 描述   | 获取当前机器人型号信息，如"GBT-P7A-700" |
| 请求参数 | 无参数                        |
| 返回值   | string: 机器人型号如"GBT-P7A-700"    [StatusCode][#3.1]: 函数执行结果    |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取机器人型号
        (string info, code) = controller.GetArmModelInfo();
        Console.WriteLine("Model: " + info);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.5 获取机器人运行状态

| 方法名  | **GetRobotState**()                    |
| ---- | -------------------------------------- |
| 描述   | 获取机器人运行状态|
| 请求参数 | 无参数                                    |
| 返回值   | [RobotState][#3.2]: 机器人运行状态   [StatusCode][#3.1]: 函数执行结果|

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取机器人运行状态
        (RobotState state, code) = controller.GetRobotState();
        Console.WriteLine("State: " + state);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.6 获取当前控制器运行状态

| 方法名  | **GetCtrlState**()                      |
| ---- | --------------------------------------- |
| 描述   | 获取当前控制器运行状态 |
| 请求参数 | 无参数                                     |
| 返回值   | [CtrlState][#3.3]: 控制器运行状态  [StatusCode][#3.1]: 函数执行结果   |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取控制器运行状态
        (CtrlState state, code) = controller.GetCtrlState();
        Console.WriteLine("State: " + state);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.7 获取当前伺服状态

| 方法名  | **GetServoState**()                   |
| ---- | ------------------------------------- |
| 描述   | 获取当前伺服状态 |
| 请求参数 | 无参数                                   |
| 返回值   | [ServoState][#3.4]: 伺服控制器状态    [StatusCode][#3.1]: 函数执行结果  |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取伺服运行状态
        (ServoState state, code) = controller.GetServoState();
        Console.WriteLine("State: " + state);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.8  获取机器人控制器版本

| 方法名  | **GetVersion**()                          |
| ---- | ----------------------------------------- |
| 描述   | 获取当前机器人控制器版本 |
| 请求参数 | 无参数                                       |
| 返回值   | string: 控制器版本     [StatusCodeEnum][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取机器人控制器版本
        (string version, code) = controller.GetVersion();
        Console.WriteLine("Version: " + version);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.9  设置机械臂的LED指示灯

| 方法名  | **SwitchLedLight**( bool `mode` )                          |
| ---- | ----------------------------------------- |
| 描述   | 设置机械臂的LED指示灯 |
| 请求参数 | `mode`: 布尔值，表示打开或关闭LED指示灯                                       |
| 返回值   | 运行结果： 详见[接口返回状态码][#3.1]         |
| 兼容性   | 协作机器人控制器版本 1.3.6 及以上版本，工业机器人不支持         |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 关闭灯光
        code = controller.SwitchLedLight(false);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.10 让机器人伺服上电

| 方法名  | **Execution.ServoOn**() |
| ---- | ------------- |
| 描述   | 让机械臂伺服上电      |
| 请求参数 | 无参数           |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 机械臂伺服上电
        code = controller.Execution.ServoOn();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.11 让机器人伺服下电

| 方法名  | **Execution.ServoOff**() |
| ---- | -------------- |
| 描述   | 让机器人伺服下电       |
| 请求参数 | 无参数            |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 机械臂伺服上电
        code = controller.Execution.ServoOff();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.1.12 让机器人伺服重置

| 方法名  | **Execution.ServoReset**() |
| ---- | ---------------- |
| 描述   | 让机器人伺服重置         |
| 请求参数 | 无参数              |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 机械臂伺服重置
        code = controller.Execution.ServoReset();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.2 机器人运动控制和状态

### 4.2.1 获取机器人参数

#### 4.2.1.1 获取 OVC 全局速度比率

| 方法名  | **Motion.GetOVC**()                |
| ---- | --------------------------------- |
| 描述   | 获取 OVC 全局速度比率     |
| 请求参数 | 无                                                 |
| 返回值   | double: 全局速度比率  [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.1.2 获取 OAC 全局加速度比率

| 方法名  | **Motion.GetOAC**()                |
| ---- | --------------------------------- |
| 描述   | 获取 OAC 全局加速度比率     |
| 请求参数 | 无                                                 |
| 返回值   | double: 全局加速度比率  [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.1.3 获取当前使用的 TF

| 方法名  | **Motion.GetTF**()                |
| ---- | --------------------------------- |
| 描述   | 获取当前使用的 TF      |
| 请求参数 | 无                                                 |
| 返回值   | int: TF序号  [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.1.4 获取当前使用的 UF

| 方法名  | **Motion.GetUF**()                |
| ---- | --------------------------------- |
| 描述   | 获取当前使用的 UF      |
| 请求参数 | 无                                                 |
| 返回值   | int: UF序号  [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.1.5 获取当前使用的 TCS 示教坐标系

| 方法名  | **Motion.GetTCS**()                |
| ---- | --------------------------------- |
| 描述   | 获取当前使用的 TCS 示教坐标系      |
| 请求参数 | 无                                                 |
| 返回值   | [TCSType][#3.8]: TCS类型  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取参数
        (double res, code) = controller.Motion.GetOVC();
        if (code == StatusCode.OK)
        {
            Console.WriteLine($"OVC = {res}");
        }

        (TCSType type, code) = controller.Motion.GetTCS();
        if (code == StatusCode.OK)
        {
            Console.WriteLine($"TCSType = {(TCSType)type}");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.2 设置机器人参数

#### 4.2.2.1 设置 OVC 全局速度比率

| 方法名  | **Motion.SetOVC**( double `value` )   |
| ---- | ---------------------------------------- |
| 描述   | 设置 OVC 全局速度比率        |
| 请求参数 | `value`: double, 速度比率范围是0~1  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.2.2 设置 OAC 全局加速度比率

| 方法名  | **Motion.SetOAC**( double `value` )   |
| ---- | ---------------------------------------- |
| 描述   | 设置 OAC 全局加速度比率        |
| 请求参数 | `value`: double, 速度比率范围是0~1.2  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.2.3 设置当前使用的TF

| 方法名  | **Motion.SetTF**( int `value` )   |
| ---- | ---------------------------------------- |
| 描述   | 设置当前使用的TF        |
| 请求参数 | `value`: int, TF序号, 0~10之间  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.2.4 设置当前使用的UF

| 方法名  | **Motion.SetUF**( int `value` )   |
| ---- | ---------------------------------------- |
| 描述   | 设置当前使用的UF        |
| 请求参数 | `value`: int, UF序号, 0~10之间  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

#### 4.2.2.5 设置当前使用的TCS

| 方法名  | **Motion.SetTCS**( TCSType `value` )   |
| ---- | ---------------------------------------- |
| 描述   | 设置当前使用的TCS        |
| 请求参数 | `value`: [TCSType][#3.8], UF序号, 0~10之间  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取参数
        code = controller.Motion.SetTF(2);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Set TF Success");
        }
        
        code = controller.Motion.SetTCS(TCSType.TOOL);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Set TCS Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.3 将笛卡尔点位转换成关节值点位

| 方法名  | **Motion.ConvertCartToJoint**( [MotionPose][#3.9] `pose`, int `ufIndex` = 0, int `tfIndex` = 0 )    |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 描述   | 将笛卡尔点位转换成关节值点位                 |
| 请求参数 | `pose`: [MotionPose][#3.9] 机器人的位姿   `ufIndex`: int 用户坐标系id  `tfIndex`: int 工具坐标系id |
| 返回值   | [MotionPose][#3.9]: 机器人的位姿  [StatusCode][#3.1]: 函数执行结果|

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

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

        // Act
        (MotionPose convertPose, StatusCode code) = motionManager.ConvertCartToJoint(motionPose);
        if (code == StatusCode.OK)
        {
            Console.WriteLine(convertPose);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.4 将关节值点位转换成笛卡尔点位

| 方法名  | **Motion.ConvertJointToCart**( MotionPose `pose`, int `ufIndex` = 0, int `tfIndex` = 0 )    |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 描述   | 将关节值点位转换成笛卡尔点位      |
| 请求参数 | `pose`: [MotionPose][#3.9] 机器人的位姿   `ufIndex`: int 用户坐标系id  `tfIndex`: int 工具坐标系id |
| 返回值   | [MotionPose][#3.9]: 机器人的位姿  [StatusCode][#3.1]: 函数执行结果|

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        MotionPose motionPose = new MotionPose();
        motionPose.Pt = PoseType.Joint;
        motionPose.Joint = new Joint{
            J1 = 0,
            J2 = 0,
            J3 = 60,
            J4 = 60,
            J5 = 0,
            J6 = 0
        };

        // Act
        (MotionPose convertPose, StatusCode code) = motionManager.ConvertJointToCart(motionPose);

        if (code == StatusCode.OK)
        {
            Console.WriteLine(convertPose);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.5 机器人末端移动到指定的位置

| 方法名  | Motion.MoveJoint( MotionPose `pose`, double `vel` = 1, double `acc` = 1 )   |
| ---- | --------------------------------------------------------- |
| 描述   | 让机器人末端移动到指定的位置                |
| 请求参数 | `pose`: [MotionPose][#3.9] 笛卡尔空间或关节坐标系上的一个点的坐标   `vel`: float 运动的速度，范围是0~1, 表示最大速度的倍数  `acc`: float 范围是0~1.2, 表示最大加速度的倍数|
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        MotionPose motionPose = new MotionPose();
        motionPose.Pt = PoseType.Joint;
        motionPose.Joint = new Joint{
            J1 = 0,
            J2 = 0,
            J3 = 60,
            J4 = 60,
            J5 = 0,
            J6 = 0
        };

        // Act
        code = motionManager.MoveJoint(motionPose);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Move Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.6 让机器人末端沿直线移动到指定的位置

| 方法名   | Motion.MoveLine(MotionPose `pose`, double `vel` = 100, double `acc` = 1) |
| -------- | ------------------------------------------------------------ |
| 描述     | 让机器人末端沿直线移动到指定的位置                           |
| 请求参数 | `pose`: [MotionPose][#3.9] 笛卡尔空间或关节坐标系上的一个点的坐标   `vel`: float 运动的速度，范围是0~5000mm/s, 表示机械臂末端移动速度  `acc`: float 范围是0~1.2, 表示最大加速度的倍数 |
| 返回值   | [StatusCodeEnum][#3.1]: 函数执行结果                         |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        MotionPose motionPose = new MotionPose();
        motionPose.Pt = PoseType.Joint;
        motionPose.Joint = new Joint{
            J1 = 0,
            J2 = 0,
            J3 = 60,
            J4 = 60,
            J5 = 0,
            J6 = 0
        };

        // Act
        code = motionManager.MoveLine(motionPose);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Move Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.7 机器人末端沿直线移动到指定的位置

| 方法名  | Motion.MoveCircle(MotionPose `pose1`, MotionPose `pose2`, double vel = 100, double acc = 1)   |
| ---- | ---------------------------------------------- |
| 描述   | 让机器人末端沿弧线移动到指定的位置                       |
| 请求参数 | `pose1`: [MotionPose][#3.9] 机械臂运动的途径点位姿  `pose2`: [MotionPose][#3.9] 机械臂运动的终点位姿   `vel`: float 运动的速度，范围是0~5000mm/s, 表示机械臂末端移动速度  `acc`: float 范围是0~1.2, 表示最大加速度的倍数 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        MotionPose motionPose1 = MotionPose.GenerateRandomPose(PoseType.Joint);

        MotionPose motionPose2 = MotionPose.GenerateRandomPose(PoseType.Joint);

        // 移动到指定姿态
        code = controller.Motion.MoveCircle(motionPose1, motionPose2);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Move Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.8 获取机器人的当前位姿

| 方法名  | **Motion.GetCurrentPose**(PoseType `pt`, int `ufIndex` = 0, int `tfIndex` = 0)    |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 描述   | 获取机器人的当前位姿                    |
| 请求参数 | `pose_type`:[PoseType][#3.12] 位姿类型   `ufIndex`: 当使用PoseType.CART时需传入用户坐标系id, 默认0  `tfIndex` : 当使用PoseType.CART时需传入工具坐标系id, 默认0 |
| 返回值   | [MotionPose][#3.9]: 机器人位姿  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取机器人的当前位姿
        (MotionPose motionPose, code) = controller.Motion.GetCurrentPose(PoseType.Cart, 0, 0);
        if (code == StatusCode.OK)
        {
            Console.WriteLine(motionPose);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.9 获取机器人的DH参数

| 方法名  | **Motion.GetDHParam**() |
| ---- | ----------------------- |
| 描述   | 获取机器人的DH参数    |
| 请求参数 | 无参数              |
| 返回值   | List<[DHparam][#3.13]>: DH参数列表  [StatusCode][#3.1]: 函数执行结果 |

### 4.2.10 设置机器人的DH参数

| 方法名  | Motion.SetDHParam(List<[DHparam][#3.13]> `dHparams`) |
| ---- | ---------------------------- |
| 描述   | 设置机器人的DH参数                   |
| 请求参数 | `dHparams` [DHparam][#3.7]列表  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取参数
        (List<DHparam> dhParamsList, StatusCode code1) = controller.Motion.GetDHParam();
        if (code1 == StatusCode.OK)
        {
            Console.WriteLine("Get Success");
        }

        // 设置参数
        code = controller.Motion.SetDHParam(dhParamsList);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Set Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.11 获取机器人轴锁定状态

| 方法名  | Motion.GetDragSet()            |
|------|----------------------------------------------------------------------------------|
| 描述   | 获取当前机器人轴锁定状态                           |
| 请求参数 | 无参数                                        |
| 返回值  | [DragStatus][#3.16]: 轴锁定状态，Ture表示该轴为可移动状态，False表示被锁定 [StatusCode][#3.1]: 函数执行结果 |

### 4.2.12 设定机器人轴锁定状态

| 方法名  | Motion.SetDragSet(DragStatus `dragStatus`)                 |
|------|-------------------------------------------------------|
| 描述   | 设定当前机器人轴锁定状态                                          |
| 请求参数 | `dragStatus`: [DragStatus][#3.16] 轴锁定状态，默认全部为Ture:解锁状态 |
| 返回值  | [StatusCode][#3.1]: 函数执行结果                                |

### 4.2.13 设定当前机器人拖动状态

| 方法名  | Motion.EnableDrag(bool `dragState`)             |
|------|------------------------------------------------|
| 描述   | 设定当前机器人轴锁定状态                                   |
| 请求参数 | `dragState`: bool 机器人的拖动状态，true表示进入拖动状态，false表示退出拖动状态 |
| 返回值  | [StatusCode][#3.1]: 函数执行结果                         |
| 兼容性   | 协作机器人控制器版本 1.3.2 及以上版本，工业机器人 1.2.1 及以上版本         |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取当前机器人的轴锁定状态
        (DragStatus dragStatus, StatusCode code2) = controller.Motion.GetDragSet();
        if (code2 == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 修改当前机器人的轴锁定状态d
        dragStatus.CartStatus.X = false;
        dragStatus.IsContinuousDrag = true;
        code2 = controller.Motion.SetDragSet(dragStatus);
        if (code2 == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 启动拖动
        code = controller.Motion.EnableDrag(true);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Execute Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.14 进入实时位置控制模式

| 方法名  | **Motion.EnterPositionControl**() |
| ---- | ---------------------------- |
| 描述   | 进入实时位置控制模式，允许对机器人进行精确的位置控制 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果                    |
| 备注   | 在进入实时控制模式后，必须通过UDP发送控制指令 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

### 4.2.15 退出实时位置控制模式

| 方法名  | **Motion.ExitPositionControl**() |
| ---- | ---------------------------- |
| 描述   | 退出实时位置控制模式，恢复默认的机器人控制状态 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果                    |
| 备注   | 退出后，机器人将不再接受实时控制指令 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

### 4.2.16 设置订阅参数

| 方法名  | Motion.SetUDPFeedbackParams( bool `flag`, string `ip`, int `interval`, int `feedbackType`, List<[int](#3.100)> `DOList` = null ） |
| ---- | ---------------------------- |
| 描述   | 配置机器人向指定IP地址推送数据的订阅参数 |
| 请求参数 | `flag`：bool 是否开启UDP数据推送；`ip`：string 接收端的IP地址；`interval`：int 发送数据的间隔（单位：毫秒）；`feedbackType`：int 反馈数据格式（0：XML格式）；`DOList`：list<[int](#3.100)> 期望获取的DO信号列表（最多十个，可选） |
| 返回值   | [StatusCode][#3.1]: 函数执行结果                    |
| 备注   | 参数设置仅在UDP数据推送功能启用时有效 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

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

### 4.2.17 获取机器人软限位

| 方法名  | **Motion.GetUserSoftLimit**()             |
|------|------------------------------------------------|
| 描述   | 获取机器人软限位                                   |
| 请求参数 | 无|
| 返回值  | List(List(double)): 机器人软限位信息, 列表第一层代表各轴，第二层代表每个轴的下限位和上限位值  [StatusCode][#3.1]: 函数执行结果                         |

示例代码

```cs
using Agilebot.IR;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取机器人软限位
        (List<List<double>> res, StatusCode code2) = motionManager.GetUserSoftLimit();
        if (code2 == StatusCode.OK)
        {
            Console.WriteLine(res);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.2.18 指定UDP输出位置控制的相关参数

| 方法名  | Motion.SetPositionTrajectoryParams(int `maxTimeoutCount`, int `timeout`, double `wristElbowThreshold`, double `shoulderThreshold`)             |
|------|------------------------------------------------|
| 描述   | 指定UDP输出位置控制的相关参数                                   |
| 请求参数 | `maxTimeoutCount`：最大超时次数； `timeout`：超时时间（即发送间隔，默认为20ms）； `wristElbowThreshold`：腕/肘部接近奇异点的阈值； `shoulderThreshold`：接近肩部奇异点的阈值；|
| 返回值  | [StatusCode][#3.1]: 函数执行结果                         |

### 4.2.19 负载相关接口

#### 4.2.19.1 获取当前激活的负载

| 方法名  | **Motion.Payload.GetCurrentPayload**() |
| ---- | ---------------------------- |
| 描述   | 获取当前激活的负载信息 |
| 请求参数 | 无  |
| 返回值   | int: 当前激活负载的索引  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.2 激活对应的负载

| 方法名  | **Motion.Payload.SetCurrentPayload**( int `index` ) |
| ---- | ---------------------------- |
| 描述   | 激活对应的负载 |
| 请求参数 | `index`：负载索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 负载id必须是当前设备中存在的 |

#### 4.2.19.2 获取所有负载信息

| 方法名  | **Motion.Payload.GetAllPayloadInfo**() |
| ---- | ---------------------------- |
| 描述   | 获取所有负载的详细信息 |
| 请求参数 | 无  |
| 返回值   | Dictionary\<uint, string>: 返回负载信息字典  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.3 添加负载

| 方法名  | **Motion.Payload.AddPayload**( PayloadInfo `payload` ) |
| ---- | ---------------------------- |
| 描述   | 添加新的负载 |
| 请求参数 | `payload`: [PayloadInfo][#3.6] 负载对象 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 新的负载id必须是当前设备中没有的且在1~10之间 |

#### 4.2.19.4 删除指定负载

| 方法名  | **Motion.Payload.DeletePayload**( int `index` ) |
| ---- | ---------------------------- |
| 描述   | 删除指定索引的负载 |
| 请求参数 | `index`: int 负载索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 负载id必须是当前设备中存在的 |

#### 4.2.19.5更新指定负载

| 方法名  | **Motion.Payload.UpdatePayload**( PayloadInfo `payload` ) |
| ---- | ---------------------------- |
| 描述   | 更新指定负载信息 |
| 请求参数 | `payload`: [PayloadInfo][#3.6] 负载对象 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 负载id必须是当前设备中存在的 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Motion;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取负载列表
        (Dictionary<uint, string> payloadList, code) = controller.Motion.Payload.GetAllPayloadInfo();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Success");
        }

        // 添加负载
        PayloadInfo payload = new()
        {
            Id = 6,
            Comment = "test",
            Weight = 1,
            MassCenter = new() { X = 1, Y = 2, Z = 3 },
            InertiaMoment = new() { LX = 10, LY = 20, LZ = 30 }
        };

        code = controller.Motion.Payload.AddPayload(payload);

        // 设置当前激活的负载
        code = controller.Motion.Payload.SetCurrentPayload(6);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

#### 4.2.19.6 检测3轴是否水平

| 方法名  | **Motion.Payload.CheckAxisThreeHorizontal**() |
| ---- | ---------------------------- |
| 描述   | 检测3轴是否水平 |
| 请求参数 | 无  |
| 返回值   | double: 3轴的水平角度  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 水平的角度，必须在-1~1之间才能进行负载测定 |

#### 4.2.19.7 获取负载测定状态

| 方法名  | **Motion.Payload.GetPayloadIdentifyState**() |
| ---- | ---------------------------- |
| 描述   | 获取负载测定的状态 |
| 请求参数 | 无  |
| 返回值   | [PayloadIdentifyState][#3.7]: 负载测定状态  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.8 开始负载测定

| 方法名  | **Motion.Payload.StartPayloadIdentify**(double `weight`, double `angle`) |
| ---- | ---------------------------- |
| 描述   | 开始负载测定 |
| 请求参数 | `weight`：负载重量（未知重量填-1）  `angle`：6轴允许转动的角度（30-90度） |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 开始负载测定前必须先进入负载测定状态 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持    |

#### 4.2.19.9 获取负载测定结果

| 方法名  | **Motion.Payload.PayloadIdentifyResult**() |
| ---- | ---------------------------- |
| 描述   | 获取负载测定的结果 |
| 请求参数 | 无  |
| 返回值   | [PayloadInfo][#3.6]: 返回负载测定结果  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.10 开始干涉检查

| 方法名  | **Motion.Payload.InterferenceCheckForPayloadIdentify**(double `weight`, double `angle`) |
| ---- | ---------------------------- |
| 描述   | 开始负载测定的干涉检查, 用于查看是否会发生碰撞  |
| 请求参数 | `weight`：负载重量；`angle`：6轴转动角度（30-90度） |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.11 进入负载测定状态

| 方法名  | **Motion.Payload.PayloadIdentifyStart**() |
| ---- | ---------------------------- |
| 描述   | 进入负载测定状态 |
| 请求参数 | 无  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.12 结束负载测定状态

| 方法名  | **Motion.Payload.PayloadIdentifyDone**() |
| ---- | ---------------------------- |
| 描述   | 结束负载测定状态 |
| 请求参数 | 无  |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

#### 4.2.19.13 负载测定全流程

| 方法名  | **Motion.Payload.PayloadIdentify**( double `weight` = -1, double `angle` = 90 ) |
| ---- | ---------------------------- |
| 描述   | 完整的负载测定流程 |
| 请求参数 | `weight`：负载重量（未知重量填-1）；`angle`：6轴转动角度（30-90度） |
| 返回值   | 返回负载测定结果[PayloadInfo][#3.6][StatusCode][#3.1]: 函数执行结果 |
| 备注   | 返回的负载可以新增到机器人中或写入机器人中已有的某个负载  全流程步骤： 1.进入负载测定状态 2.开始负载测定 3.获取负载测定结果 4.结束负载测定状态|
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Motion;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 执行负载测定
        (PayloadInfo payload, code) = controller.Motion.Payload.PayloadIdentify(weight, angle);

        payload.data.id = 6;

        // 保存负载到机器人中
        code = controller.Motion.Payload.AddPayload(payload);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.3 机器人操作类

### 4.3.1 执行某个指定的程序

| 方法名  | Execution.Start(string `programName`)  |
| ---- | ---------------------------------------- |
| 描述   | 执行某个指定的程序                         |
| 请求参数 | `programName`: string 需要执行的程序名称 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果        |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";

        // 运行"test"程序
        code = controller.Execution.Start(progName);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Start Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.3.2 停止某个程序执行

| 方法名  | Execution.Stop(string `programName` = null)  |
| ---- | ---------------------- |
| 描述   | 停止某个程序执行或停止当前运动               |
| 请求参数 | `programName`: string  需要停止的程序名称, 不传参时默认控制当前运行程序或正在执行的动作 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";

        // 停止"test"程序
        code = controller.Execution.Stop(progName);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Stop Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.3.3 返回所有正在运行的程序详细信息

| 方法名  | **Execution.AllRunningPrograms**() |
| ---- | ------------------------ |
| 描述   | 返回所有正在运行的程序详细信息          |
| 请求参数 | 无参数                      |
| 返回值   | Dictionary\<string, int>: 运行的程序ID和程序名列表  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取所有正在运行的程序详细信息
        (Dictionary<string,int> progList, code) = controller.Execution.AllRunningPrograms();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Get All Running Programs Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.3.4 暂停某个程序的运行

| 方法名  | Execution.Pause(string programName = null) |
| ---- | -------------------------------------- |
| 描述   | 暂停某个程序的运行或暂停当前运动              |
| 请求参数 | programName: string 需要暂停的程序名称, 不传参时默认控制当前运行程序或正在执行的动作 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";

        // 暂停"test"程序
        code = controller.Execution.Pause(progName);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Pause Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.3.5 继续运行某个处于暂停状态的程序

| 方法名  | **Execution.Resume**(programName)  |
| ---- | ------------------------ |
| 描述   | 继续运行某个处于暂停状态的程序或恢复当前运动          |
| 请求参数 | programName: string 需要继续运行的程序名称, 不传参时默认控制当前运行程序或正在执行的动作 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";

        // 继续运行"test"程序
        code = controller.Execution.Resume(progName);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Resume Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.3.6 执行BAS脚本程序

| 方法名  | Execution.ExecuteBasScript(BasScript `script`) |
| ---- | ------------------------ |
| 描述   | 执行BAS脚本程序        |
| 请求参数 | `script`: BasScript 程序脚本[接口返回状态码][#3.1] |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | BAS脚本程序的暂停、恢复、停止方法同普通程序 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持  |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 创建脚本程序
        BasScript script = new BasScript("test");
        StatusCode code = script.MoveJoint(MovePoseType.PR, 1, SpeedType.VALUE, 100, SmoothType.FINE);

        // 执行脚本程序
        code = execution.ExecuteBasScript(script);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Resume Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.4 程序信息读写

### 4.4.1 获取一个程序中指定序号的机器人pose点位值

| 方法名  | ProgramPoses.Read(string `programName`, int `index`, FileType `ft` = FileType.UserProgram)               |
| ---- | ------------------------------------------- |
| 描述   | 获取一个程序中指定序号的Pose的值  见         |
| 请求参数 | `programName`: string 指定程序名  `index`: int 指定pose的序号  `ft`: [FileType][#3.18] 文件类型  |
| 返回值   | [ProgramPose][#3.17]程序中的机器人位姿   [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";
        int index = 1;

        // 读取"test"程序中第一个
        (ProgramPose pose, code) = controller.ProgramPoses.Read(progName, index);
        if (code == StatusCode.OK)
        {
            Console.WriteLine(pose);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.4.2 修改一个程序中指定序号的机器人Pose点位值

| 方法名  | ProgramPoses.Write(string `programName`, int `index`, ProgramPose `value`, FileType `ft` = FileType.UserProgram)                |
| ---- | ----------------------------------------------------------------------------------- |
| 描述   | 更新一个程序中指定序号的Pose的值      |
| 请求参数 | `programName`: string 指定程序名  `index`: int 指定pose的序号  `value`: [ProgramPose][#3.17] 程序中的机器人位姿  `ft`: [FileType][#3.18] 文件类型        |
| 返回值   |[StatusCode][#3.1]: 函数执行结果             |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";
        int index = 1;
        ProgramPose rndPose = ProgramPose.GenerateRandomPose(index);

        // 更新"test"程序中第一个
        code = controller.ProgramPoses.Write(progName, index, rndPose);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Write Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.4.3 添加一个程序中指定序号的机器人Pose点位值

| 方法名  | **ProgramPoses.Add**(string `programName`, int `index`, ProgramPose `value`, FileType `ft` = FileType.UserProgram)         |
| ---- | ----------------------------------------------------------------------------------- |
| 描述   | 添加一个程序中指定序号的Pose的值         |
| 请求参数 | `programName`: string 指定程序名   `index`: int 指定pose的序号  `value`: [ProgramPose][#3.17] 程序中的机器人位姿  `ft`: [FileType][#3.18] 文件类型        |
| 返回值   |[StatusCode][#3.1]: 函数执行结果  |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";
        int index = 1;
        ProgramPose rndPose = ProgramPose.GenerateRandomPose(index);

        // 更新"test"程序中第一个
        code = controller.ProgramPoses.Add(progName, index, rndPose);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Add Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.4.4 删除一个程序中指定序号的机器人Pose点位值

| 方法名  | **ProgramPoses.Delete**(string `programName`, int `index`, FileType `ft` = FileType.UserProgram)              |
| ---- | ------------------------------------------- |
| 描述   | 删除一个程序中指定序号的Pose的值                        |
| 请求参数 | `programName`: string 指定程序名    `index`: int 指定pose的序号  `ft`: [FileType][#3.18] 文件类型 |
| 返回值   |[StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";
        int index = 1;
        ProgramPose rndPose = ProgramPose.GenerateRandomPose(index);

        // 删除"test"程序中第一个
        code = controller.ProgramPoses.Delete(progName, index);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Delete Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.4.5 获取一个程序中所有的机器人Pose点位值

| 方法名  | **ProgramPoses.ReadAllPoses**(string `programName`, FileType `ft` = FileType.UserProgram)    |
| ---- | -------------------------------- |
| 描述   | 获取一个程序中所有的机器人Pose点位值  返回Pose点位列表 |
| 请求参数 | `programName`: string 指定程序名  `ft`: [FileType][#3.18] 文件类型               |
| 返回值   |[StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";

        // 读取"test"程序中所有位姿
        (List<ProgramPose> poses, code) = controller.ProgramPoses.ReadAllPoses(progName);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Read Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.4.6 用于将Cart或Joint类型的机器人pose点位值相互转换

| 方法名  | **ProgramPoses.ConvertPose**(ProgramPose pose, PoseType toType)                                |
| ---- | ------------------------------------------------------------------------------- |
| 描述   | 用于将程序中机器人位姿P在坐标系类型Cart和Joint之间转换                                                |
| 请求参数 | pose: [ProgramPose][#3.17] 程序中的机器人位姿  to\_type: [`PoseType`][#3.12]  希望转换后的类型 |
| 返回值   | 位姿信息 [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ProgramPoses;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string progName = "test";
        int cartIndex = 1;
        (ProgramPose cartPose, code) = controller.ProgramPoses.Read(progName, cartIndex);

        // 转换位姿
        (ProgramPose pose, code) = controller.ProgramPoses.ConvertPose(cartPose, PoseType.Joint);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Convert Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.5  IO信号

### 4.5.1 读取指定类型指定端口IO的值

| 方法名  | **Signals.Read**(SignalType `type`, int `index`)                        |
| ---- | -------------------------------------------- |
| 描述   | 读取指定类型指定端口IO的值    |
| 请求参数 | `type`: [SignalType][#3.19] 要读取的IO类型    `index`: int 要读取的IO的序号，从1开始 |
| 返回值   | IO值：int，1代表高电平，0代表低电平  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        SignalType type = SignalType.DI;
        int index = 1;

        // 读取IO
        (int res, code) = controller.Signals.Read(type, index);
        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Read Success: {type}：{index} has value {res}");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.5.2 写指定类型指定端口IO的值

| 方法名  | **Signals.Write**(SignalType `type`, int `index`, double `value`)          |
| ---- | --------------------------------------------------------------------------------------- |
| 描述   | 写指定类型指定端口IO的值              |
| 请求参数 | `type`: [SignalType][#3.19] 要写入的IO类型    `index`: 要写入的IO的序号，从1开始  `value`: 要写入的值 1代表高电平 0代表低电平 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        SignalType type = SignalType.DO;
        int index = 1;
        int value = 1;

        // 写入IO
        code = controller.Signals.Write(type, index, value);
        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Write Success: {type}：{index} has value {value}");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.6 寄存器信息

### 4.6.1 R 寄存器相关操作

| 方法名  | **Registers.Read\_R**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取R寄存器的值     |
| 请求参数 | `index`: 希望获取的寄存器编号       |
| 返回值   | double: 寄存器值  [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Write\_R**(int `index`, double `value`)                 |
| ---- | ------------------------------- |
| 描述   | 写入R寄存器的值     |
| 请求参数 | `index`: int 希望写入的寄存器编号  `value`: double R寄存器的值    |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Delete\_R**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 删除R寄存器     |
| 请求参数 | `index`: 希望删除的寄存器编号       |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Registers;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        int index = 1;

        // 读取
        (double value, code) = controller.Registers.Read_R(index);
        code = registers.Write_R(index, 9.9);
        code = registers.Delete_R(index);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.6.2 MR 寄存器相关操作

| 方法名  | **Registers.Read\_MR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取MR寄存器的值     |
| 请求参数 | `index`: 希望获取的寄存器编号       |
| 返回值   | int: 寄存器值  [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Write\_MR**(int `index`, int `value`)                 |
| ---- | ------------------------------- |
| 描述   | 写入MR寄存器的值     |
| 请求参数 | `index`: int 希望写入的寄存器编号  `value`: int MR寄存器的值    |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Delete\_MR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 删除MR寄存器     |
| 请求参数 | `index`: 希望删除的寄存器编号       |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Registers;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        int index = 1;

        // 读取
        (int value, code) = controller.Registers.Read_MR(index);
        code = registers.Write_MR(index, 9);
        code = registers.Delete_MR(index);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.6.3 SR 寄存器相关操作

| 方法名  | **Registers.Read\_SR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取SR寄存器的值     |
| 请求参数 | `index`: 希望获取的寄存器编号       |
| 返回值   | string: 寄存器值  [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Write\_SR**(int `index`, string `value`)                 |
| ---- | ------------------------------- |
| 描述   | 写入SR寄存器的值     |
| 请求参数 | `index`: int 希望写入的寄存器编号  `value`: string SR寄存器的值    |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Delete\_SR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 删除SR寄存器     |
| 请求参数 | `index`: 希望删除的寄存器编号       |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Registers;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        int index = 1;

        // 读取
        (string value, code) = controller.Registers.Read_SR(index);
        code = registers.Write_SR(index, "test");
        code = registers.Delete_SR(index);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.6.3 PR 寄存器相关操作

| 方法名  | **Registers.Read\_PR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取PR寄存器的值     |
| 请求参数 | `index`: 希望获取的寄存器编号       |
| 返回值   | [PoseRegister][#3.20]: 寄存器值  [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Write\_PR**(int `index`, PoseRegister `value`)                 |
| ---- | ------------------------------- |
| 描述   | 写入PR寄存器的值     |
| 请求参数 | `index`: int 希望写入的寄存器编号  `value`: [PoseRegister][#3.20] PR寄存器的值    |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Delete\_PR**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 删除PR寄存器     |
| 请求参数 | `index`: 希望删除的寄存器编号       |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.Registers;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        int index = 1;

        // 读取
        (PoseRegister value, code) = controller.Registers.Read_PR(index);
        code = registers.Write_PR(index, value);
        code = registers.Delete_PR(index);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.6.5 获取MH、MI寄存器的值

| 方法名  | **Registers.Read\_MH**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取MH寄存器的值|
| 请求参数 | `index`: int 希望获取的寄存器编号               |
| 返回值   | 寄存器信息 [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Read\_MI**(int `index`)                 |
| ---- | ------------------------------- |
| 描述   | 获取MI寄存器的值|
| 请求参数 | `index`: int 希望获取的寄存器编号               |
| 返回值   | 寄存器信息 [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ModbusRegisters;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        int index = 1;

        // 读取
        (int value1, code) = controller.Registers.Read_MH(index);
        (int value2, code) = controller.Registers.Read_MI(index);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Read Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.6.6 更新一个MH、MI寄存器的值

| 方法名  | **Registers.Write\_MH**(int `index`, int `value`)    |
| ---- | ------------------------------------------------------- |
| 描述   | 更新一个MH寄存器的值                                   |
| 请求参数 | `index`: int 寄存器的编号   `value`: int 需要更新的寄存器信息 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **Registers.Write\_MI**(int `index`, int `value`)     |
| ---- | ------------------------------------------------------- |
| 描述   | 更新一个MI寄存器的值                                   |
| 请求参数 | `index`: int 寄存器的编号   `value`: int 需要更新的寄存器信息 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.ModbusRegisters;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 写入
        code = controller.Registers.Write_MH(index, 8);
        code = controller.Registers.Write_MI(index, 9);

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Write Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.7 轨迹控制

### 4.7.1 设置待执行的离线轨迹文件

| 方法名  | **Trajectory.SetOffLineTrajectoryFile**(string `path`)  |
| ---- | ---------------------------------------|
| 描述   | 设置离线轨迹文件      |
| 请求参数 | `path`: string 设置离线轨迹文件名，如示例文件A.trajectoryA.trajectory 轨迹文件格式为**文本文件**，说明如下：  - 第1行：6代表6个轴，0.001代表两个点之间间隔1ms ，8093代表一共8093个轨迹点 。  - 第二行：表示6个轴的起始位置 。  - 3-8095行: 表示轨迹点，包括6个轴的位置 、速度 、加速度 、力矩前馈、do端口、do端口的值    - do\_port代表使用的do端口（取值范围1-24）。    - do\_port 为-1， 表示在该位置不会触发IO信号。    - do\_port为1， do\_state为1， 则表明do1 端口会在该位置触发ON 信号    - do\_port为1， do\_state为0， 则表明do1 端口会在该位置触发OFF 信号   用户通过FileManager.upload将离线文件发送到机器人控制器根目录， 用4.7.2和4.7.3指令执行轨迹。 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.7.2 让机器人以安全速度移动到离线轨迹中的起始点

| 方法名  | **Trajectory.PrepareOfflineTrajectory**() |
| ---- | ------------------------------ |
| 描述   | 让机器人以安全速度移动到离线轨迹中的起始点          |
| 请求参数 | 无参数                            |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.7.3 让机器人开始执行离线轨迹文件

| 方法名  | **Trajectory.ExecuteOfflineTrajectory**() |
| ---- | ------------------------------ |
| 描述   | 让机器人开始执行离线轨迹程序                 |
| 请求参数 | 无参数                            |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.7.4 轨迹文件转换功能

| 方法名  | **Trajectory.TransformCsvToTrajectory**()              |
| ---- | ------------------------------------------- |
| 描述   | 将轨迹csv文件转换成trajectory格式的轨迹文件并存放在控制柜的轨迹文件目录上 |
| 请求参数 | 无参数                                         |
| 返回值   | 字符串：转换后文件名 [StatusCode][#3.1]: 函数执行结果 |

### 4.7.5 查询TransformCsvToTrajectory流程工作状态

| 方法名  | **Trajectory.CheckTransformStatus**() |
| ---- | -------------------------- |
| 描述   | 让机器人以安全速度移动到离线轨迹中的起始点      |
| 请求参数 | 无参数                        |
| 返回值   | 转换状态：[轨迹转换状态][#3.5] [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        string csvFilename = "test.csv";
        
        // 上传需要转换的轨迹csv文件
        code = controller.FileManger.Upload(csvFilename, FileType.TrajectoryProgram);
        // 转换轨迹
        (string trajFileName, code) = controller.Trajectory.TransformCsvToTrajectory(csvFilename);
        // 查询转换状态
        (TransformState state, code) = controller.Trajectory.CheckTransformStatus(trajFileName);
        Console.WriteLine(state);
        // 设置轨迹文件
        code = controller.Trajectory.SetOffLineTrajectoryFile(trajFileName);
        // 移动到离线轨迹中的起始
        code = controller.Trajectory.PrepareOfflineTrajectory();
        
        // 等待机器人运动完成
        RobotState robotState = RobotState.ROBOT_RUNNING;
        while (robotState != RobotState.ROBOT_IDLE)
        {
            (robotState, code) = controller.GetRobotState();
            Thread.Sleep(1000);
        }
        
        // 执行轨迹
        code = controller.Trajectory.ExecuteOfflineTrajectory();

        if (code == StatusCode.OK)
        {
            Console.WriteLine($"Delete Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.8 报警信息

### 4.8.1 获取最严重的一条报警

| 方法名  | **Alarm.GetTopAlarm**() |
| ---- | ----------------- |
| 描述   | 获取最严重的一条报警        |
| 请求参数 | 无参数               |
| 返回值   | string: 报警信息  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取最严重的一条报警
        (string topError, code) = controller.Alarm.GetTopAlarm();
        if (code == StatusCode.OK)
        {
            Console.WriteLine(topError);
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.8.2 获取所有的活动的报警

| 方法名  | **Alarm.GetAllActiveAlarm**()   |
| ---- | ------------------------- |
| 描述   | 获取所有的活动的报警 |
| 请求参数 | 无参数                       |
| 返回值   | List(string): 报警信息列表  [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 获取所有的活动的报警
        (List<string> errors, code) = controller.Alarm.GetAllActiveAlarm();
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Get All Active Alarm Success");
        }

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

### 4.8.3 复位错误

| 方法名  | **Alarm.ResetAlarms**()   |
| ---- | ------------------------- |
| 描述   | 复位错误 |
| 请求参数 | 无参数                       |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

***

## 4.9 文件服务类

### 4.9.1 上传本地文件到机器人

| 方法名  | **Upload**(string `filePath`, FileType `ft`, bool `overWriting` = false)      |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 描述   | 上传本地文件到机器人                                                                                                                                       |
| 请求参数 | `filePath`: string 需要上传的本地文件的绝对路径  `ft`: [FileType][#3.18] 上传的文件类型  `overWriting`: bool 是否覆盖写机器人已存在的文件 默认不覆盖写 |
| 备注   | USER\_PROGRAM和BLOCK\_PROGRAM文件上传只需填写程序名，无需填写后缀        |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.9.2 下载机器人文件到本地

| 方法名  | **Download**(string `fileName`, FileType `ft`, string `savePath`)         |
| ---- | ----------------------------------------------------- |
| 描述   | 下载机器人文件到本地                |
| 请求参数 | `fileName`: string 要下载的文件名 无需带后缀  `ft`: [FileType][#3.18] 要下载的文件类型   `savePath`: 下载文件的本地保存路径 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.9.3 删除机器人上的文件

| 方法名  | **Delete**(string `fileName`, FileType `ft`)         |
| ---- | --------------------------------------------------------- |
| 描述   | 删除机器人上的文件     |
| 请求参数 | `fileName`: string 要下载的文件名 无需带后缀  `ft`: [FileType][#3.18] 要删除的文件类型 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.9.4 用户提供一个pattern 查找机器人上符合pattern模式的文件

| 方法名  | **Search**(string `pattern`, ref List<[string]()> `fl`)              |
| ---- | ------------------------------------------- |
| 描述   | 查找控制器上符合pattern模式的文件                        |
| 请求参数 | `pattern`: 文件名称适配字符串  `fl`: 返回的文件列表 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

***

## 4.10 BasScript脚本程序类

| 方法名  | **BasScript**(name)|
| ---- | ------------------------- |
| 描述   | 对应示教器程序编写中的程序指令 |
| 请求参数 | name：脚本程序名 |
| 兼容性   | 协作机器人控制器版本 1.3.7 及以上版本，工业机器人不支持         |

### 4.10.1 MoveJoint指令

| 方法名  | **BasScript.MoveJoint**(poseType, poseIndex, speedType, speedValue, smoothType, smoothDistance, extraParam)   |
| ---- | ------------------------- |
| 描述   | 对应示教器程序编写中的MoveJoint指令 |
| 请求参数 | poseType：位姿类型    poseIndex：位姿索引  speedType：速度类型  speedValue：速度值  smoothType：平滑类型  smoothDistance：平滑距离  extraParam：附加参数 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.2 MoveLine指令

| 方法名  | **BasScript.MoveLine**(poseType, poseIndex, speedType, speedValue, smoothType, smoothDistance, extraParam)   |
| ---- | ------------------------- |
| 描述   | 对应示教器程序编写中的MoveLine指令 |
| 请求参数 | poseType：位姿类型    poseIndex：位姿索引  speedType：速度类型  speedValue：速度值  smoothType：平滑类型  smoothDistance：平滑距离  extraParam：附加参数 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.3 MoveCircle指令

| 方法名  | **BasScript.MoveCircle**(poseType1, poseIndex1, poseType2, poseIndex2, speedType, speedValue, smoothType, smoothDistance, extraParam)   |
| ---- | ------------------------- |
| 描述   | 对应示教器程序编写中的MoveCircle指令 |
| 请求参数 | poseType1：途径点位姿类型    poseIndex1：途径点位姿索引  poseType2：终点位姿类型    poseIndex2：终点位姿索引  speedType：速度类型  speedValue：速度值  smoothType：平滑类型  smoothDistance：平滑距离  extraParam：附加参数 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.4 ExtraParam类

| 方法名  | **ExtraParam.Acceleration**(value)   |
| ---- | ------------------------- |
| 描述   | 附加加速度设定 |
| 请求参数 | value：加速度值，1~120之间 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **ExtraParam.RTCP**()   |
| ---- | ------------------------- |
| 描述   | RTCP设定 |
| 请求参数 | 无参数 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **ExtraParam.Offset**(index)   |
| ---- | ------------------------- |
| 描述   | 坐标偏移设定 |
| 请求参数 | index：偏移用的PR索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **ExtraParam.TB**(second, type, name)   |
| ---- | ------------------------- |
| 描述   | 在当前指令运行后执行程序指令 |
| 请求参数 | second：延时秒数  type：指令类型  name：程序名称 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **ExtraParam.TB**(second, type, index, status)   |
| ---- | ------------------------- |
| 描述   | 在当前指令运行后给指定IO赋值 |
| 请求参数 | second：延时秒数  type：IO类型  index：IO索引  status：要赋予的状态 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

| 方法名  | **ExtraParam.SKIP**(index)   |
| ---- | ------------------------- |
| 描述   | 设置跳转指令 |
| 请求参数 | index：跳转到指定的LABEL序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.5 AssignValue指令

| 方法名  | **BasScript.AssignValue**(param1, index, param2, value, optIndex, optValue)   |
| ---- | ------------------------- |
| 描述   | 赋值指令 |
| 请求参数 | param1：参数1类型  index：参数1索引  param2：参数2类型  value：参数2值  optIndex：参数1附加索引  optValue：参数2附加值 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.6 AssignValue指令

| 方法名  | **BasScript.AssignValue**(param, index, value)   |
| ---- | ------------------------- |
| 描述   | 为变量赋值 |
| 请求参数 | param：参数类型（AssignType）  index：索引（整数）  value：值（IOStatus、double或string） |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.BasScript;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 生成脚本程序
        BasScript script = new BasScript("test");
        code = script.MoveJoint(MovePoseType.PR, 1, SpeedType.VALUE, 25, SmoothType.FINE);
        BasScript.ExtraParam param = new();
        param.Acceleration(80);
        code = script.MoveJoint(MovePoseType.PR, 2, SpeedType.VALUE, 50, SmoothType.FINE, extraParam: param);

        // 执行脚本程序
        code = controller.Execution.ExecuteBasScript(script);

        // 关闭连接
        code = controller.Disconnect();
    }
}

```

### 4.10.7 LogiIf指令

| 方法名  | **BasScript.LogiIf**(param1, index, param2, value, operatorType)   |
| ---- | ------------------------- |
| 描述   | 为变量赋值 |
| 请求参数 | param1：第一个参数，类型为RegisterType或IOType  index：索引（整数）  param2：第二个参数，类型为RegisterType、IOType或OtherType  value：值，类型为索引、数值、字符串或IOStatus  operatorType：布尔操作符，默认为等于|
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.8 LogiElseIf指令

| 方法名  | **BasScript.LogiElseIf**(param1, index, param2, value, operatorType)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 ELSE IF 语句到脚本中 |
| 请求参数 | param1：第一个参数，类型为RegisterType或IOType  index：索引（整数）  param2：第二个参数，类型为RegisterType、IOType或OtherType  value：值，类型为索引、数值、字符串或IOStatus  operatorType：布尔操作符，默认为等于|
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.9 LogiElse指令

| 方法名  | **BasScript.LogiElse**()   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 ELSE 语句到脚本中 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.10 LogiEndIf指令

| 方法名  | **BasScript.LogiEndIf**()   |
| ---- | ------------------------- |
| 描述   | 结束逻辑 IF 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.BasScript;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 生成脚本程序
        BasScript script = new BasScript("test");
        code = script.LogiIf(RegisterType.R, 1, OtherType.VALUE, 1);
        code = script.MoveJoint(MovePoseType.PR, 1, SpeedType.VALUE, 25, SmoothType.FINE);
        code = script.LogiElseIf(RegisterType.R, 1, OtherType.VALUE, 2);
        code = script.MoveJoint(MovePoseType.PR, 2, SpeedType.VALUE, 50, SmoothType.FINE);
        code = script.LogiElse();
        code = script.MoveJoint(MovePoseType.PR, 3, SpeedType.VALUE, 50, SmoothType.FINE);
        code = script.LogiEndIf();

        // 执行脚本程序
        code = controller.Execution.ExecuteBasScript(script);

        // 关闭连接
        code = controller.Disconnect();
    }
}

```

### 4.10.11 LogiWhile指令

| 方法名  | **BasScript.LogiWhile**(param1, index, param2, value, operatorType)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 WHILE 语句到脚本中 |
| 请求参数 | param1：第一个参数，类型为RegisterType或IOType  index：索引（整数）  param2：第二个参数，类型为RegisterType、IOType或OtherType  value：值，类型为索引、数值、字符串或IOStatus  operatorType：布尔操作符，默认为等于|
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.12 LogiEndWhile指令

| 方法名  | **BasScript.LogiEndWhile**()   |
| ---- | ------------------------- |
| 描述   | 结束逻辑 While 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;
using Agilebot.IR.BasScript;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 生成脚本程序
        BasScript script = new BasScript("test");
        code = script.LogiWhile(IOType.DO, 1, OtherType.IO_STATUS, IOStatus.ON);
        code = script.MoveJoint(MovePoseType.PR, 1, SpeedType.VALUE, 25, SmoothType.FINE);
        code = script.LogiEndWhile();

        // 执行脚本程序
        code = controller.Execution.ExecuteBasScript(script);

        // 关闭连接
        code = controller.Disconnect();
    }
}

```

### 4.10.13 LogiSwitch指令

| 方法名  | **BasScript.LogiSwitch**(param, index)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 SWITCH 语句到脚本中 |
| 请求参数 | param：参数，类型为 RegisterType 或 IOType  index：参数的索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.14 LogiCase指令

| 方法名  | **BasScript.LogiCase**(param, value)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 CASE 语句到脚本中 |
| 请求参数 | param：参数，类型为 RegisterType、IOType 或 OtherType  value：值，类型为索引、数值、字符串 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.15 LogiDefault指令

| 方法名  | **BasScript.LogiDefault**()   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 DEFAULT 语句到脚本中 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.16 LogiEndSwitch指令

| 方法名  | **BasScript.LogiEndSwitch**()   |
| ---- | ------------------------- |
| 描述   | 结束逻辑 SWITCH 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.17 LogiSkipCondition指令

| 方法名  | **BasScript.LogiSkipCondition**(param1, index, param2, value, operatorType)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 SKIP CONDITION 语句到脚本中 |
| 请求参数 | param1：第一个参数，类型为RegisterType或IOType  index：参数一的索引  param2：第二个参数，类型为RegisterType、IOType或OtherType  value：值，类型为索引、数值、字符串或IOStatus  operatorType：布尔操作符，默认为等于 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.18 Wait指令

| 方法名  | **BasScript.Wait**(param1, index, param2, value, operatorType)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 WAIT COND 语句到脚本中 |
| 请求参数 | param1：第一个参数，类型为RegisterType或IOType  index：参数一的索引  param2：第二个参数，类型为ValuesType、IOType或OtherType  value：值，类型为索引、数值、字符串或IOStatus  operatorType：布尔操作符，默认为等于 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.19 WaitTime指令

| 方法名  | **BasScript.WaitTime**(param, value)   |
| ---- | ------------------------- |
| 描述   | WAIT TIME 等待一定时间 |
| 请求参数 | param：参数类型  value：等待的时间值 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.20 LogiGoto指令

| 方法名  | **BasScript.LogiGoto**(index)   |
| ---- | ------------------------- |
| 描述   | GOTO 跳转语句 |
| 请求参数 | index：目标标签的索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.21 LogiLabel指令

| 方法名  | **BasScript.LogiLabel**(index)   |
| ---- | ------------------------- |
| 描述   | LABEL 语句 |
| 请求参数 | index：标签的索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.22 LogiBreak指令

| 方法名  | **BasScript.LogiBreak**()   |
| ---- | ------------------------- |
| 描述   | BREAK 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.23 LogiContinue指令

| 方法名  | **BasScript.LogiContinue**()   |
| ---- | ------------------------- |
| 描述   | CONTINUE 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.24 Pause指令

| 方法名  | **BasScript.Pause**()   |
| ---- | ------------------------- |
| 描述   | PAUSE 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.25 Abort指令

| 方法名  | **BasScript.Abort**()   |
| ---- | ------------------------- |
| 描述   | ABORT 语句 |
| 请求参数 | 无 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.26 Call指令

| 方法名  | **BasScript.Call**(name)   |
| ---- | ------------------------- |
| 描述   | CALL 同步调用程序 |
| 请求参数 | name：程序名 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.27 Run指令

| 方法名  | **BasScript.Run**(name)   |
| ---- | ------------------------- |
| 描述   | RUN 异步调用程序 |
| 请求参数 | name：程序名 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.28 Load指令

| 方法名  | **BasScript.Load**(param, value)   |
| ---- | ------------------------- |
| 描述   | LOAD 载入程序 |
| 请求参数 | param：参数，R寄存器、SR寄存器、数值或字符串  value：参数的值，数值或字符串 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.29 Unload指令

| 方法名  | **BasScript.Unload**(param, value)   |
| ---- | ------------------------- |
| 描述   | UNLOAD 卸载程序 |
| 请求参数 | param：参数，R寄存器、SR寄存器、数值或字符串  value：参数的值，数值或字符串 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.30 Exec指令

| 方法名  | **BasScript.Exec**(param, value)   |
| ---- | ------------------------- |
| 描述   | EXEC 执行程序 |
| 请求参数 | param：参数，R寄存器、SR寄存器、数值或字符串  value：参数的值，数值或字符串 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.31 SocketOpen指令

| 方法名  | **BasScript.SocketOpen**(index)   |
|### 4.10.13 LogiSwitch指令

| 方法名  | **BasScript.LogiSwitch**(param, index)   |
| ---- | ------------------------- |
| 描述   | 添加一个逻辑 SWITCH 语句到脚本中 |
| 请求参数 | param：参数，类型为 RegisterType 或 IOType  index：参数的索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.32 SocketClose指令

| 方法名  | **BasScript.SocketClose**(index)   |
| ---- | ------------------------- |
| 描述   | SOCKET CLOSE 关闭 socket 连接 |
| 请求参数 | index：SK寄存器序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.33 SocketConnect指令

| 方法名  | **BasScript.SocketConnect**(index)   |
| ---- | ------------------------- |
| 描述   | SOCKET CONNECT 连接 socket |
| 请求参数 | index：SK寄存器序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.34 SocketSend指令

| 方法名  | **BasScript.SocketSend**(index, msgType, value)   |
| ---- | ------------------------- |
| 描述   | SOCKET SEND 通过 socket 发送数据 |
| 请求参数 | index：SK寄存器序号  msgType：消息类型  value：消息内容或序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.35 SocketRecv指令

| 方法名  | **BasScript.SocketRecv**(index, msgLength, msgType, value)   |
| ---- | ------------------------- |
| 描述   | SOCKET RECV 接收 socket 数据 |
| 请求参数 | index：SK寄存器序号  msgLength：消息长度  msgType：消息类型  value：消息内容或序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.36 ModbusReadMH指令

| 方法名  | **BasScript.ModbusReadMH**(index, id, address, length, rIndex)   |
| ---- | ------------------------- |
| 描述   | ReadMH 读取 Modbus 保持寄存器 |
| 请求参数 | index：通道序号  id：Modbus ID  address：寄存器地址  length：寄存器长度  rIndex：写入的 R 寄存器序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.37 ModbusReadMI指令

| 方法名  | **BasScript.ModbusReadMI**(index, id, address, length, rIndex)   |
| ---- | ------------------------- |
| 描述   | ReadMI 读取 Modbus 输入寄存器 |
| 请求参数 | index：通道序号  id：Modbus ID  address：寄存器地址  length：寄存器长度  rIndex：写入的 R 寄存器序号 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.38 ModbusWriteMH指令

| 方法名  | **BasScript.ModbusWriteMH**(index, id, address, length, valueType, value)   |
| ---- | ------------------------- |
| 描述   | ModbusWriteMH 用于写入 Modbus 保持寄存器 |
| 请求参数 | index：通道序号  id：Modbus ID  address：寄存器地址  length：寄存器长度  valueType：值类型  value：值或索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.39 VisionFind指令

| 方法名  | **BasScript.VisionFind**(name)   |
| ---- | ------------------------- |
| 描述   | VISION FIND 寻找视觉程序 |
| 请求参数 | name：视觉程序名称 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.40 VisionGetOffset指令

| 方法名  | **BasScript.VisionGetOffset**(name, index, labelIndex)   |
| ---- | ------------------------- |
| 描述   | VISION GET OFFSET 获取视觉程序偏移量 |
| 请求参数 | name：视觉程序名称  index：视觉寄存器索引  labelIndex：标签索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.41 VisionGetQuantity指令

| 方法名  | **BasScript.VisionGetQuantity**(name, index)   |
| ---- | ------------------------- |
| 描述   | VISION GET QUANTITY 获取视觉程序结果 |
| 请求参数 | name：视觉程序名称  index：R寄存器索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.10.42 SetParam指令

| 方法名  | **BasScript.SetParam**(type, valueType, value)   |
| ---- | ------------------------- |
| 描述   | SET PARAM 设置参数 |
| 请求参数 | type：参数类型  valueType：值类型  value：值 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

***

## 4.11 坐标系类

### 4.11.1 获取指定坐标系信息

| 方法名  | **CoordinateSystem.Get**(CoordinateType `type`, int `index`) |
| ---- | ---------------------------- |
| 描述   | 根据用户传入的索引，获取对应的坐标系信息 |
| 请求参数 | `type`: [CoordinateType][#3.22.1] 坐标系类型；  `index`: int 坐标系索引 |
| 返回值   | 返回坐标系信息（`Coordinate`）  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

***

### 4.11.2 更新坐标系信息

| 方法名  | **CoordinateSystem.Update**(CoordinateType `type`, Coordinate `coordinate`) |
| ---- | ---------------------------- |
| 描述   | 根据用户传入的坐标系信息，更新指定的坐标系 |
| 请求参数 | `type`: [CoordinateType][#3.22.1] 坐标系类型；  `coordinate`: [Coordinate][#3.22] 要写入的坐标系信息 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

***

### 4.11.3 添加坐标系信息

| 方法名  | **CoordinateSystem.Add**(CoordinateType `type`, Coordinate `coordinate`) |
| ---- | ---------------------------- |
| 描述   | 根据用户提供的坐标系信息，添加一个新的坐标系 |
| 请求参数 | `type`: [CoordinateType][#3.22.1] 坐标系类型；  `coordinate`: [Coordinate][#3.22] 要写入的坐标系信息 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

***

### 4.11.4 删除指定坐标系信息

| 方法名  | **CoordinateSystem.Delete**(CoordinateType `type`, int `index`)) |
| ---- | ---------------------------- |
| 描述   | 根据用户传入的索引，删除对应的坐标系信息 |
| 请求参数 | `type`: [CoordinateType][#3.22.1] 坐标系类型；  `index`: int 坐标系索引 |
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

***

### 4.11.5 获取坐标系信息列表

| 方法名  | **CoordinateSystem.GetCoordinateList**(CoordinateType `type`) |
| ---- | ---------------------------- |
| 描述   | 根据用户传入的坐标系类型，  获取所有坐标系信息的列表 |
| 请求参数 | `type`: [CoordinateType][#3.22.1] 坐标系类型 |
| 返回值   | `List` \[CoordSummary]\[#3.22.2]: 返回坐标系信息列表（）  [StatusCode][#3.1]: 函数执行结果 |
| 备注   | 无 |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);
        // 尝试连接
        StatusCode code = await controller.Connect();

        // 生成坐标系
        Coordinate coord = new Coordinate();
        coord.data.name = "test";
        coord.data.id = 5;
        coord.data.group_id = 1;
        coord.data.comment = "test_comment";
        coord.data.data = new Coordinate.Pos
        {
            data = new List<double>
                        {
                            11,
                            22,
                            33,
                            44,
                            55,
                            66
                        }
        };

        // 添加坐标系
        code = controller.CoordinateSystem..Add(CoordinateType.UserCoordinate, coord);

        // 删除坐标系
        code = controller.CoordinateSystem..Delete(CoordinateType.UserCoordinate, 5);

        // 关闭连接
        code = controller.Disconnect();
    }
}
```

***

## 4.12 机器人示教运动

### 4.12.1 机器人Jogging运动

| 方法名  | **Jogging.Move**(int `ajNum`, MoveMode `moveMode`, double `stepLength` = 0) |
| ---- | ---------------------------- |
| 描述   | 机器人示教运动                  |
| 请求参数 | `ajNum`: int需要运动的轴序号，正代表正方向运动，负代表负方向运动  `moveMode`: MoveMode 运动模式，包括连续运动和单步运动   `stepLength`: double 步长，单位为mm或角度(仅在单步运动模式下有效)|
| 返回值   | [StatusCode][#3.1]: 函数执行结果 |

### 4.12.2 停止机器人Jogging运动

| 方法名  | **Jogging.Stop**() |
| ---- | ---------------------------- |
| 描述   | 停止机器人示教运动                 |
| 请求参数 | 无  |
| 返回值   | 无  |
| 备注   | 仅运动模式为连续运动时需要使用  |

示例代码

```cs
using Agilebot.IR;
using Agilebot.IR.Types;

public class Test
{
    public static async Task Main()
    {
        string controllerIP = "10.27.1.254";
        Arm controller = new Arm(controllerIP);

        // 尝试连接
        StatusCode code = await controller.Connect();

        // 启动连续运动
        code = controller.Jogging.Move(3, MoveMode.Continuous);
        if (code == StatusCode.OK)
        {
            Console.WriteLine("Move Success");
        }
        
        // 运动3秒
        Thread.Sleep(3000);

        // 停止
        controller.Jogging.Stop();

        // 关闭连接
        code = controller.Disconnect();
    }
}
```
