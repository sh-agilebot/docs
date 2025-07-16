---
url: /zh/1-python/AgileBot_Robot_Python_SDK_ChangeLog.md
---
# 捷勃特机器人 Python SDK 更新说明

## 1.7.0.0更新（2025/5/30）

1. 寄存器改动
   1. 寄存器全部放在Registers类下，其他Registers后续废除
   2. 接口名改为read\_R、write\_R、delete\_R类似
   3. 删除add方法，使用write\_XX即可
   4. 读取和写入寄存器RPC接口改为新的仅读取值的RPC，提升速度
   5. read\_R、read\_MR、read\_SR直接返回对应的值和执行结果

2. arm类下接口改动
   1. get\_arm\_model\_info、get\_ctrl\_status、get\_robot\_status、get\_servo\_status、get\_soft\_mode、get\_version接口改为返回 '结果+执行状态'
   2. servo\_on、servo\_off、servo\_reset接口移到arm下，execution下后续废除

3. motion类改动
   1. paload相关操作接口移到到 motion.payload 下
   2. 新增负载测定相关接口
   3. 新增get\_OVC、set\_OVC、get\_OAC、set\_OAC、get\_TF、set\_TF、get\_UF、set\_UF、get\_TCS、set\_TCS接口
   4. convert\_cart\_to\_joint\_simple 接口新增uf\_index和tf\_index设置
   5. 新增move\_joint、move\_line、move\_circle接口
   6. 新增convert\_joint\_to\_cart、convert\_cart\_to\_joint接口
   7. 新增enter\_position\_control、exit\_position\_control、set\_udp\_feedback\_params接口

4. digital\_signals 类改为 signals 类，简化名称

5. execution类添加execute\_bas\_script接口用于执行脚本

6. jogging.move接口添加步进值修改 move(*self*, *aj\_num*: *int*, *move\_mode*: MoveMode = None, *step\_length*: *float* = 0)

7. 新增bas\_script类用于生成脚本

8. 新增modbus类用于直接控制modbus设备

## 1.7.1.3更新（2025/7/3）

1. 修复 get\_all\_active\_alarms 接口可能发生错误的问题
2. 修复 move\_circle 内部参数设置错误
3. 修改示例程序
4. 添加插件管理类，提供 extension.get\_robot\_ip 接口
5. 添加轨迹复现相关接口
