
## 导出 iOS 平台
### 在 Xcode 导出可执行文件时，已添加 `GMESDK.framework` 库，编译时出现编译报错，如何解决？

工程文件中选择 Build Setting，在 "Other Linker Flags" 中，如果有使用 “-all_load” 标志，请尝试删掉并重新编译。


### Unity 导出 XCode 工程后，出现 `framework not found GMESDK` 错误，该如何解决？

使用 Unity 引擎请接入 GME Unity SDK，使用 `libGMESDK.a` 库，不需要使用 framework 文件。

### 使用 Unity SDK 后，导出 iOS 可执行文件时报错，提示与 armv7 相关，删除 armv7 后恢复正常，如何解决？

- 建议升级 Unity 版本，详情请参见 [Unity 官网](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516)。
- 若您无需升级，则不打包 armv7 架构即可。

### 下载 iOS Demo 后无法运行，如何解决？

下载官方 iOS Demo 后，在 Xcode（版本为10以上） 编译时出现类似 `ld: warning: directory not found for option` 等错误，需手动将 Demo 同级目录下 “GME_SDK” 中的 “GMESDK.framework” 文件添加到工程的 Framework 列表中。


### iOS SDK 是否支持模拟器调试？

支持。请用官网 [最新包 ](https://intl.cloud.tencent.com/document/product/607/18521) 进行验证。

### 导出 Demo 的时候出现证书错误，如何解决？
报错信息如下：
```
Showing Recent Messages:-1: Unity-iPhone has conflicting provisioning settings. Unity-iPhone is automatically signed, but code signing identity iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd has been manually specified. Set the code signing identity value to "iPhone Developer" in the build settings editor, or switch to manual signing in the project editor. (in target 'Unity-iPhone')
```
解决方案：
请真机导出时，将腾讯云的企业证书替换为您的开发者证书。


### 导出真机时候出现以下错误，应该如何解决？
报错信息如下：
```
dyld: Library not loaded: @rpath/libLamemp3.framework/libLamemp3
Referenced from: /private/var/containers/Bundle/Application/XXXX
Reason: image not found
dyld: launch, loading dependent libraries
DYLD_LIBRARY_PATH=/usr/lib/system/introspection
DYLD_INSERT_LIBRARIES=/Developer/usr/lib/libBacktraceRecording.dylib:/Developer/usr/lib/libMainThreadChecker.dylib:/Developer/Library/PrivateFrameworks/DTDDISupport.framework/libViewDebuggerSupport.dylib
```
解决方案：
- 若使用动态库，加载的动态库默认在静态库 `Linked Frameworks and Libraries` 下，需要选中它，并单击它下面的 `-` 号进行删除；重新单击 `Embedded Binaries` 下面的 `+` 增加动态库。
- 或者将 framework 修改为如图所示：
![](https://main.qcloudimg.com/raw/fe01a75aba37436d4cae1dd68b3b9640.jpg)


## 导出 Windows 平台

### 下载 Unity Demo 导出 PC 可执行文件时报错，如何处理？

如果使用过程中有 `Found plugins with same names and architectures` 类似报错，因为 GME SDK 默认同时提供 x86 和 x86_64 架构的 SDK 版本，请在 plugins 文件夹中删除其中一份。


### 下载 Unreal Demo 导出 PC 可执行文件时提示找不到 dll，如何解决？

以导出 Windows x64 版本为例，导出可执行文件之后，将工程目录 `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` 下的 dll 文件全量拷贝到可执行文件（.exe）同目录下。

## Android 导出问题

### 集成 GME SDK 并导出 Apk 后，启动程序发生黑屏现象，如何解决？

问题在于缺失了某些 lib 文件，请解压 Apk 后查看 lib 下的各个文件夹中库文件是否齐全。

### 导出到 Android 手机使用的时候，点击 App 会提示不支持该设备，如何解决？

这与打包出来的可执行文件包含什么架构有关。如果不需要 v8a 架构的话，可以在 Unity 工程配置中的导出栏“取消”勾选导出 v8a 架构。

### 导出之后的 Apk 不支持模拟器，应该怎么解决？

先检查导出来的 Apk 里面是否有包含 x86 的库文件，如果没有请重新下载 SDK 后重新导入 x86 架构 SDK 文件后再导出可执行文件。




## Unity-WebGL 导出问题

### Unity-WebGL 平台需要使用 https 协议还是 http 协议？
打包出来的产物需要通过**https协议**进行部署，如果使用http协议部署到服务端，功能会出现异常。

### Unity-WebGL 平台打包后，进房出现 1004 错误。
进房报1004(Invalid Argument)的错误，这是因为填入的 Openid 小于10000。这里需要填入的 **Openid 大于10000**。

### Unity-WebGL 平台打包后可以用于手机端吗？
根据 Unity 官网所述，Unity-WebGL 打包的产物暂时不支持手机端运行，详见 [Unity - Manual: WebGL Browser Compatibility (unity3d.com)](https://docs.unity3d.com/2020.1/Documentation/Manual/webgl-browsercompatibility.html)。

### Unity-WebGL 平台打包后，可以使用 GME 的范围语音功能吗？
目前WebGL平台只支持最简单的实时语音通话的功能：进退房，开关麦的功能。对于不支持的功能，调用接口会返回1006的错误码。范围语音功能目前正在适配 WebGL 平台。
