## Overview

To help you use CLS more efficiently, we have created SDKs in multiple programming languages for log upload. You can choose an appropriate version based on your business needs.

## Precautions

- The SDK encapsulates the data access APIs of CLS uniformly to make log upload much easier.
- The SDK implements the encapsulation of CLS logs in the Protobuf format, so you don't need to care about the specific details of this format when writing logs.
- The SDK implements the compression methods defined in CLS APIs, so you don't need to care about the details of compression implementation. SDKs for certain programming languages support writing compressed logs by default.
- The SDK provides unified features such as async sending, resource control, automatic retry, graceful shutdown, and log perception to make log reporting more comprehensive.


## SDK List

The following table lists the source code of CLS SDKs for different programming languages at GitHub:


| SDK Language | GitHub Source Code |
|---------|---------|
| Java | [tencentcloud-cls-sdk-java](https://github.com/TencentCloud/tencentcloud-cls-sdk-java)  |
| C++ | [tencentcloud-cls-sdk-c++](https://github.com/TencentCloud/tencentcloud-cls-sdk-cpp) |
| Go | [tencentcloud-cls-sdk-go](https://github.com/TencentCloud/tencentcloud-cls-sdk-go)  |
| NodeJS | [tencentcloud-cls-sdk-js](https://github.com/TencentCloud/tencentcloud-cls-sdk-js)   |
| Android | [tencentcloud-cls-sdk-android](https://github.com/TencentCloud/tencentcloud-cls-sdk-android) |
| iOS | [tencentcloud-cls-sdk-ios](https://github.com/TencentCloud/tencentcloud-cls-sdk-ios) |

