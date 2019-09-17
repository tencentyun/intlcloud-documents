# SDK集成指南

## 简介
本文档提供关于 SDK 的接入以及 demo 的使用方法。



## SDK 组成

SDK 目录文件和功能说明：

| **目录** | **说明** |
| --- | --- | --- |
| application | 应用入口及API使用使用样例 |
| doc | 源代码相关说明文档存放目录 |
| include | SDK头文件xgAgent.h存放目录 |
| lib |  SDK静态库libxgIoT.a存放目录 |
| Makefile | 工程管理文件 |
| README.md | SDK使用说明 |



## Demo使用方法

本使用方法基于x86_64平台，其他平台请参考相关SDK的描述文档。

SDK提供测试demo，无需修改任何代码就可以编译出demo执行文件，并使用demo进行推送测试。

## 编译Demo

1.进入Demo源码根目录，运行命令编译：

```
make
```
编译完成后，可在根目录看到xgDemo文件生成。

2.清除编译文件，运行命令：

```
make clean
```


## 启动Demo

启动时需要将accessID、accessKey、deviceName传入到测试应用，命令格式如下：
```
./xgDemo [accessID] [accessKey] [deviceName]
```
当看到下面消息时，表示设备运行成功
```xml
level":"D","message":"xgMqttRpcResult(811):cmd account "}
[20190909_20:14:44]{"time":"2019-0909-12:14:43.830","level":"D","message":"agentSetStatusFlag(297):xgStatusFlag 0x1F "}
```
## 推送消息到Demo

在控制台或使用 REST API进行消息推送，当在xgDemo日志中看到以下内容，表示推送成功。

```xml
[20190909_20:15:22][demo Debug]$$$$$$$$$$$$$$$$$$$$$$$
[20190909_20:15:22][demo Debug]Recv data 39Byte: {"audience_type":"all","Key1":"Value1"}
```



## 集成步骤

1.在SDK下载页选择IoTSDK进行下载。
2.将lib目录下的 libxgIoT.a和include目录下的xgAgent.h拷贝到自定义的源码目录中。
3.修改Makefile，在编译选项中添加

```c
-lxgIoT -lpthread -lrt
```

4.参考application目录下的 main.c 的代码将SDK的API集成到自己的源码中。

