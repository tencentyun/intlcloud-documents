## Introduction

If you want to impose restrictions on room entry for certain rooms (for example, a room can be entered only by members), and you are worried that such restrictions, if implemented on the client, would be easy to break, then you can consider **enabling room permission control**.

## Supported Platforms

| iOS | Android | macOS | Windows | WeChat Mini Program | Chrome Browser |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|     ✔  |    ✔    |    ✔   |    ✔    |   ✔    |   ✔    |

## PrivateMapKey

### Feature Overview
`privateMapKey` is an optional field in `TRTCParamEnc` used to make Tencent Cloud check whether the user has permission to enter the specified room.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)

### Difference from `UserSig`

- [**UserSig**](https://intl.cloud.tencent.com/document/product/647/35166) 
This is a required field in `TRTCParamEnc` used to check whether the current user is authorized to use the TRTC cloud service so as to prevent attackers from stealing the traffic in your `sdkappid` account.

- **privateMapKey**
This is an optional field in `TRTCParamEnc` used to check whether the current user is authorized to enter the room with the specified `roomid`. It is only necessary if your business needs to distinguish between different users.

 In addition, you can also determine whether the current user is authorized to enter the specified room directly in the application. `privateMapKey` is only to make this practice more secure as it can prevent the application from being cracked (i.e., non-members can enter high-level rooms).
 
## How to Enable
 - **Enable room permission control in the [TRTC Console](https://console.cloud.tencent.com/rav).**

 - **Calculate `privateMapKey` on your server.**
  As `privateMapKey` aims to prevent the client from being reversely cracked (i.e., non-members can enter high-level rooms), it should be calculated on your backend server and then returned to the client.
  Three samples of code for calculating `PrivateMapKey` are provided for Java, PHP, and Node.js, respectively, which can be directly downloaded and integrated into your server.

| Programming Language | Key Function | Download Link |
|:---------:|:---------:|:---------:|
| Java | `genPrivateMapKey` | [GitHub](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/java)|
| PHP | `genPrivateMapKey` | [GitHub](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/php)|
| Node.js | `genPrivateMapKey` | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/nodejs)|

 - **Distribute `privateMapKey` to your application and use it to set the `privateMapKey` parameter in `TRTCParamEnc`.**

## FAQs
 - **Why can't all online rooms be entered?**
 Once room permission control is enabled, all rooms under the current `sdkappid` can only be entered after `privateMapKey` is set in `TRTCParamEnc`, so if your online business is in operation and the relevant logic of `privateMapKey` has not been added to it, please do not enable this feature.

