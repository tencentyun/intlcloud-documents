为方便开发者快速解决开发中所遇到的问题，这里向您介绍 GME 问题处理方法。

## 常见问题指引
在开发中遇到的一些常见问题，可以分析下问题的类型后，通过以下文档进行解决：

|文档|解决的问题|
|---|----|
|[功能特性问题](https://intl.cloud.tencent.com/document/product/607/39520)|GME 功能相关的问题，例如支持的平台等等。|
|[计费相关问题](https://intl.cloud.tencent.com/document/product/607/30255)|对于计费模式有疑惑，或者对计费的时机有疑惑，可以参考这篇文档。|
|[Demo 使用问题](https://intl.cloud.tencent.com/document/product/607/39521)|使用 GME 的 SampleProject，或者体验 Demo 出现的问题。|
|[鉴权相关问题](https://intl.cloud.tencent.com/document/product/607/39824)|使用 GME 需要用到鉴权，出现问题可以参考这篇文档。|
|[实时语音进房失败问题](https://intl.cloud.tencent.com/document/product/607/39523)、[实时语音无声及音频问题](https://intl.cloud.tencent.com/document/product/607/39524)、[网络问题](https://intl.cloud.tencent.com/document/product/607/39519)|使用 GME 实时语音的过程中出现的问题，可以判断下问题的类型，参考文档进行解决。|
|[语音转文本问题](https://intl.cloud.tencent.com/document/product/607/39716)|使用语音转文本功能遇到的问题汇总。|
|[工程导出问题](https://intl.cloud.tencent.com/document/product/607/39522)|在各个平台，如果遇到导出应用出现问题，或者在真机上出现问题，可以参考进行解决。|


## 开发问题

如果在开发的过程中，出现功能性的问题，首先可以通过返回的错误码进行判断。通过错误码无法解决问题时，可通过 [工单](https://console.tencentcloud.com/workorder/category) 联系 GME 开发者协助进行分析错误，解决问题。


### 错误码

GME [错误码文档](https://intl.cloud.tencent.com/document/product/607/33223)文档中，会列出错误码数值，以及此错误码对应的原因及解决方案，可以参考进行排查问题。


### 如何取得日志？

提供日志的时候，请同时提供出现问题的相关时间点，并提供接收端（听）以及发送端（说）的日志。

**日志路径**
`QAVSDK_` 带日期的 `.log` 文件为日志文件。目录如下：

| 平台    | 路径                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | `%appdata%\GMEGLOBAL\GME\processName`                            |
| iOS     | `Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents`   |
| Android | `/sdcard/Android/data/xxx.xxx.xxx/files`                       |
| Mac     | `/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents` |

如果是使用 Unity 引擎，并且在 PC 端开发，可以尝试在 `%appdata%\Tencent\GME\Unity.exe` 路径下找到日志。

在 iOS 真机上，可以通过应用程序支持文件共享来取得日志，具体步骤如下：
1. 在应用程序的 `Info.plist` 文件中添加 UIFileSharingEnabled 键，并将键值设置为“YES”。
2. 将您希望共享的文件放在应用程序的 Documents 目录下。
3. 一旦设备插入到用户计算机，iTunes 就会在选中设备的 Apps 标签中显示一个 File Sharing 区域。
4. 此后，用户就可以向该目录添加文件或者将文件移动到桌面计算机中。

>?使用 GME2.8.4以下版本，Windows 平台日志位置为：`%appdata%\Tencent\GME\ProcessName`。

**日志等级**

提供日志时如果有调用过 SetLogLevel 设置的日志等级，建议恢复默认日志等级。


**日志加密**

目前 GME 日志默认是加密状态，可以调用接口取消加密，建议在开发阶段取消加密，上线前恢复加密。接口需要在init之前调用。

```
SetAdvanceParams("DisableEncryptLog", "1");
```

|参数|含义|
|--|--|
|参数1|填入"DisableEncryptLog"，代表取消加密相关功能|
|参数2|填入"1"表示取消日志加密，填入"0"表示保持日志加密|


## 崩溃问题


遇到崩溃问题，可以先参见 [工程导出问题](https://intl.cloud.tencent.com/document/product/607/39522) 进行处理，如无法解决，需要提供堆栈给到 GME 开发者。
- 如果已经接入了第三方异常上报插件，可以联系 GME 开发者共享崩溃堆栈链接。
- 如果是 iOS 或者 Android 平台的崩溃，可以把机器连接上电脑，通过 Xcode 或者 AndroidStudio 中的 LogCat 获取到崩溃堆栈，复制后提供给 GME 开发人员。
- 如果是 Windows 平台，请提供 DUMP 文件。
