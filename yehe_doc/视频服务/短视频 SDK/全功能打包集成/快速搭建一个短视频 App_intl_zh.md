
## 终端部分

按照如下三步操作，可以用 XCode 或者 Android Studio 编译和调试小视频 App 的客户端代码。


### step1. 下载 App 源码
单击 [小视频源码](https://intl.cloud.tencent.com/document/product/1069/37914#.E5.85.A8.E5.8A.9F.E8.83.BD.E5.B0.8F.E8.A7.86.E9.A2.91-app.EF.BC.88demo.EF.BC.89.E6.BA.90.E4.BB.A3.E7.A0.81) 可以下载到小视频 App 的源代码。

### step2. 申请 SDK 用的 License
请参考 [申请 License](https://intl.cloud.tencent.com/document/product/1069/38041)。

### step3. 准备调试环境
**iOS 平台** 
- XCode 9 或更高版本
- OS X 10.10 或更高版本

**Android 平台**
- Android NDK: android-ndk-r12b
- Android SDK Tools: android-sdk_26.0.2
  - minSdkVersion: 15
  - targetSdkVersion: 21

### step4. 编译运行
单击 XCode 或 Android Studio 的 Build 按钮，即可完成编译和运行工作，源码中默认配置了腾讯云提供的测试服务器地址`http://demo.vod2.myqcloud.com/lite/`，以便您快速在调试环境中运行我们的 App。


## 后台部分

后台部分请参考[vod-xiaoshipin-server](https://github.com/tencentyun/vod-xiaoshipin-server)