
本文主要介绍如何快速地将腾讯云视立方·移动直播 LiteAVSDK（iOS）集成到您的项目中，按照如下步骤进行配置，就可以完成 SDK 的集成工作。

## 开发环境要求
- Xcode 9.0+。
- iOS 9.0 以上的 iPhone 或者 iPad 真机。
- 项目已配置有效的开发者签名。

## 集成 LiteAVSDK
您可以选择使用 CocoaPods 自动加载的方式，或者先下载 SDK，再将其导入到您当前的工程项目中。

[](id:cocoapods)
### CocoaPods
#### 1. 安装 CocoaPods
在终端窗口中输入如下命令（需要提前在 Mac 中安装 Ruby 环境）：
```
sudo gem install cocoapods
```

#### 2. 创建 Podfile 文件
进入项目所在路径，输入以下命令行之后项目路径下会出现一个 Podfile 文件。
```
pod init
```

#### 3. 编辑 Podfile 文件
编辑 Podfile 文件，有如下有两种设置方式：
-  方式一：使用腾讯云 LiteAVSDK 的 podspec 文件路径。
<dx-codeblock>
:::  podspec
  platform :ios, '9.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_International', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_International.podspec'
  end
:::
</dx-codeblock>
-  方式二：使用 CocoaPod 官方源，支持选择版本号。
<dx-codeblock>
:::  CocoaPod
   platform :ios, '9.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_International'
   end
:::
</dx-codeblock>

#### 4. 更新并安装 SDK
在终端窗口中输入如下命令以更新本地库文件，并安装 LiteAVSDK：
```
pod install
```
或使用以下命令更新本地库版本：
```
pod update
```

pod 命令执行完后，会生成集成了 SDK 的 `.xcworkspace` 后缀的工程文件，双击打开即可。

[](id:manual)
### 手动集成
1. 下载 [LiveAVSDK](https://intl.cloud.tencent.com/document/product/1071/38150) ，下载完成后进行解压。
2. 打开您的 Xcode 工程项目，选择要运行的 target , 选中 **Build Phases** 项。
![](https://qcloudimg.tencent-cloud.cn/raw/5f0a196dd78a7858fca4f098bf3e3591.png)
3. 单击 **Link Binary with Libraries** 项展开，单击底下的【+】添加依赖库。
![](https://qcloudimg.tencent-cloud.cn/raw/2e5db146788005de31337cd266315406.png)
4. 依次添加所下载的 `TXLiteAVSDK_International.framework` 及其所需依赖库 :
```
libz.tbd
libc++.tbd
libresolv.tbd
libsqlite3.tbd
Accelerate.framework
OpenAL.framework
```
![](https://qcloudimg.tencent-cloud.cn/raw/35c813a543e281c7edb408d35731779b.png)
5. 选中 Build Settings 项，搜索 `Other Linker Flags`。添加 `-ObjC`。
![](https://main.qcloudimg.com/raw/818eedfb17f50f6041e84126fe4d76ed.png)

## 授权摄像头和麦克风使用权限
使用 SDK 的音视频功能，需要授权麦克风和摄像头的使用权限。在 App 的 Info.plist 中添加以下两项，分别对应麦克风和摄像头在系统弹出授权对话框时的提示信息。
- **Privacy - Microphone Usage Description**，并填入麦克风使用目的提示语。
- **Privacy - Camera Usage Description**，并填入摄像头使用目的提示语。

![](https://qcloudimg.tencent-cloud.cn/raw/4a5b386c2f4c240d123286de0fa6ecf3.png)

## 在工程中引入 SDK
项目代码中使用 SDK 有两种方式：
- **方式一：** 在项目需要使用 SDK API 的文件里，添加模块引用。
```
@import TXLiteAVSDK_International;
```
- **方式二：**在项目需要使用 SDK API 的文件里，引入具体的头文件。
```
#import "TXLiteAVSDK_International/TXLiteAVSDK.h"
```

## 给 SDK 配置 License 授权

登录云直播控制台，在左侧菜单中选择 **直播 SDK** > **[License 管理](https://console.intl.cloud.tencent.com/live/license)**，单击 **Get License** 获取测试用 License（详细操作请参见 [申请测试版 License](https://intl.cloud.tencent.com/document/product/1071/38546）。您会获得两个字符串：一个字符串是 LicenseURL，另一个字符串是解密 Key。

在您的 App 调用 LiteAVSDK 的相关功能之前（建议在 `- [AppDelegate application:didFinishLaunchingWithOptions:]` 中）进行如下设置：

```objc
@import TXLiteAVSDK_International;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<获取到的licenseUrl>";
    NSString * const licenceKey = @"<获取到的key>";
    
    //TXLiveBase 位于 "TXLiveBase.h" 头文件中
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

## 常见问题
**LiteAVSDK 是否支持后台运行？**

**支持**，如需要进入后台仍然运行相关功能，可选中当前工程项目，在 **Capabilities** 下设置  **Background Modes** 为 **ON**，并勾选 **Audio，AirPlay and Picture in Picture** ，如下图所示：
![](https://main.qcloudimg.com/raw/ee8a9e445c6af84b5d1cec3869ed7a3a.jpg)