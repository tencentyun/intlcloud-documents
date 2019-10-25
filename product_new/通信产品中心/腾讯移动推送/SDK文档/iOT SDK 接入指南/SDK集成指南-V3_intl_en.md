# SDK integration guide

## Overview
This document guides you how to use SDK integration and the demo.



## SDK Composition

SDK directory files and features description:

| **Directory** | **Description** |
| --- | --- | --- |
| application | The application entry and API use examples |
| doc | The directory of source code documentation |
| include | The directory of the SDK header file xgAgent.h |
| lib | The directory of the SDK static library libxgIoT.a |
| Makefile | Project management files |
| README.md | SDK use instructions |



## Using Demo

This use method is based on the x86_64 platform. For other platforms, see the corresponding SDK documentation.

SDK provides a test demo, so you can compile demo executable files without modifying any code, and use the demo to perform push testing.

## Compiling Demo

1. Go to the Demo source code root directory, and execute the compiling command:

```
make
```
After compiling, you can see in the root directory that the xgDemo file has been generated.

2. Clear the compilation file, and execute the command:

```
make clean
```


## Launching Demo

When launching, you need to pass in the accessID, accessKey, and deviceName to the test application. The command format is as follows:
```
./xgDemo [accessID] [accessKey] [deviceName]
```
The following message indicates that the device operates successfully
```xml
level":"D","message":"xgMqttRpcResult(811):cmd account "}
[20190909_20:14:44]{"time":"2019-0909-12:14:43.830","level":"D","message":"agentSetStatusFlag(297):xgStatusFlag 0x1F "}
```
## Pushing messages to Demo

You can push a message in the console or by using the REST API. If the following content is shown in the xgDemo log, the push is successful.

```xml
[20190909_20:15:22][demo Debug]$$$$$$$$$$$$$$$$$$$$$$$
[20190909_20:15:22][demo Debug]Recv data 39Byte: {"audience_type":"all","Key1":"Value1"}
```



## Integration Steps

1. In the SDK download page, select **IoTSDK** to download it.
2. Copy `libxgIoT.a` in the `lib` directory and `xgAgent.h` in the `include` directory to the custom source code directory.
3. Modify Makefile and in compilation options, add:

```c
-lxgIoT -lpthread -lrt
```

4. To integrate SDK APIs into your source code, refer to the main.c code under the application directory.

