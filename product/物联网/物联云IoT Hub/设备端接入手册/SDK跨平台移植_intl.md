[//]: # (chinagitpath:XXXXX)

The following describes how to port the device-side C-SDK to the target hardware platform.

<!--### <font color=gray>Device-side C-SDK overview</font>
-->
The SDK can be roughly divided into four parts according to the code structure:
![](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/doc/SDK代码结构v1.2.jpg)

1. Hardware abstraction layer (HAL)

This is the support functions of different abstracted embedded device operating systems for our SDK, such as the network feature, memory application and establishment of the TLS/DTLS channels.

> Note:
	
> - Implementing this part is the first step in any cross-platform porting.
	
> - Implement the HAL first during porting. The HAL provided in the C-SDK is a reference implementation based on the Linux desktop OS (Ubuntu 14.04).
		
2. SDK kernel implementation layer

This is the core implementation part of the C-SDK, which encapsulates features such as the MQTT channel based on the HAL API.

> Note:
	
> As long as the HAL is implemented, there is generally no need to care about the specific implementation of this layer of code besides debugging.

3. SDK API declaration layer

 - This includes a series of prototype declarations of C functions for writing business logic and implementing the APIs for communicating with Tencent Cloud.
 
 - 	The demo code is provided in sample, which demonstrates how to use these APIs.

4. SDK sample program

 This section provides the implementation code for the scenario-based demo for your reference.
 See below for more information regarding different layers.

### Hardware Abstraction Layer (HAL)

All HAL functions are declared in `src/sdk-impl/qcloud_iot_import.h`. The following are the HAL APIs that need to be implemented. For details, see the comments.
<!--2. `src/sdk-impl/qcloud_iot_import.h` contains the subfiles in the `imports` directory.
--><!--`3. The HAL API dependencies introduced by each feature point are listed in `src/sdk-impl/imports/qcloud_iot_import_*.h``-->

**Must be implemented:**

| No. | Function name | Description |
| ---- | ---------------------- | ---------------------------------------- |
| 1 | HAL_Free | Release memory blocks |
| 2 | HAL_Malloc | Allocate a block of memory and return a pointer pointing to the beginning of the block |
| 3 | HAL_Printf | Write formatted data to a standard output stream |
| 4 | HAL_Snprintf | Write formatted data to a string |
| 5 | HAL_UptimeMs | Retrieve the number of milliseconds that elapsed since the system has started |
| 6 | HAL_SleepMs | Sleep |
| 7 | HAL_Timer_init | Initialize the timer structure |
| 8 | HAL_Timer_remain | Check the remaining time of the given timer |
| 9 | HAL_Timer_expired | Determine whether the timer has expired |
| 10 | HAL_Timer_countdown | Start timing according to the timer in seconds |
| 11 | HAL_Timer_countdown_ms | Start timing according to the timer in milliseconds |
| 12 | HAL_Timer_current | Get the formatted string of the current time |
| 13 | HAL_TLS_Connect | Establish a TLS connection for the MQTT client |
| 14 | HAL_TLS_Disconnect | Close the TLS connection |
| 15 | HAL_TLS_Write | Write data from a TLS connection |
| 16 | HAL_TLS_Read | Read data from a TLS connection |
| 17 | HAL_MutexCreate | Create mutex |
| 18 | HAL_MutexDestroy | Destroy mutex |
| 19 | HAL_MutexLock | Lock mutex |
| 20 | HAL_MutexUnlock | Unlock mutex |

**Must be implemented only when using CoAP:**

| No. | Function name | Description |
| ---- | ---------------------- | ---------------------------------------- |
| 1 | HAL_DTLS_Connect | Establish a DTLS connection for the CoAP client; implemented only if you need to use CoAP |
| 2 | HAL_DTLS_Disconnect | Close the DTLS connection |
| 3 | HAL_DTLS_Write | Write data from a DTLS connection |
| 4 | HAL_DTLS_Read | Read data from a DTLS connection |


### SDK Kernel Implementation Layer

1. The declarations of all provided functions are listed in the header file `src/sdk-impl/qcloud_iot_export.h`.
2. The subfiles in these exports directory are included in `src/sdk-impl/qcloud_iot_export.h`.
3. The APIs provided by each feature point are listed in `src/sdk-impl/exports/qcloud_iot_export_*.h`.


### SDK API Declaration Layer + Sample Program

1. API description: [SDK API Document](https://cloud.tencent.com/document/product/634/11929)
2. Introduction to the sample program: [Quick Start](https://cloud.tencent.com/document/product/634/11912)

