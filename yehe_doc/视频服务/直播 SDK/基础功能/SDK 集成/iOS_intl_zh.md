#直播集成文档_iOS

[原文地址](https://github.com/tencentyun/qcloud-documents/edit/master/product/%E8%A7%86%E9%A2%91%E6%9C%8D%E5%8A%A1/%E7%A7%BB%E5%8A%A8%E7%9B%B4%E6%92%AD/%E5%9F%BA%E7%A1%80%E5%8A%9F%E8%83%BD/SDK%20%E9%9B%86%E6%88%90/iOS.md)

本文主要介绍如何快速地将腾讯云移动直播 LiteAVSDK（iOS）集成到您的项目中。

## 开发环境要求
- Xcode 9.0+。
- iOS 9.0 以上的 iPhone 或者 iPad 真机。
- 项目已配置有效的开发者签名。

## 集成 LiteAVSDK
您可以选择使用 CocoaPods 自动加载的方式，或者先下载 SDK，再将其导入到您当前的工程项目中。

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
/// TODO TXLiteAVSDK_International.podspec仓库创建，仓库地址替换；或者删除这种方式，只保留[手动集成](#手动集成)。
```
  platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_International', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_International.podspec'
  end
```

-  方式二：使用 CocoaPod 官方源，支持选择版本号。

```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_International'
   end
```

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


### 手动集成
1. 下载 [LiveAVSDKV2](https://intl.cloud.tencent.com/document/product/1071/38150) ，下载完成后进行解压。

2. 打开您的 Xcode 工程项目，选择要运行的 target , 选中 **Build Phases** 项。
![](	https://main.qcloudimg.com/raw/81404ea4ae84f577941c0ede791eb205.png)

3. 单击 **Link Binary with Libraries** 项展开，单击底下的“+”添加依赖库。
![](https://main.qcloudimg.com/raw/940265f2e206619d249077db5f29800b.png)

4. 依次添加所下载的 `TXLiteAVDemo_International.framework` 及其所需依赖库 :
/// TODO 检查依赖库确认是否是下面这些，如果不是替换内容和图片替换
```
libz.tbd
libc++.tbd
libresolv.tbd
libsqlite3.tbd
Accelerate.framework
OpenAL.framework
```
![](https://main.qcloudimg.com/raw/899f02c77d58f6e3b9a5d94995c767f8.png)

## 授权摄像头和麦克风使用权限
使用 SDK 的音视频功能，需要授权麦克风和摄像头的使用权限。在 App 的 Info.plist 中添加以下两项，分别对应麦克风和摄像头在系统弹出授权对话框时的提示信息。
- **Privacy - Microphone Usage Description**，并填入麦克风使用目的提示语。
- **Privacy - Camera Usage Description**，并填入摄像头使用目的提示语。

![](https://main.qcloudimg.com/raw/16760a062247ee5acf117bb60ee791fc.png)

## 在工程中引入 SDK
项目代码中使用 SDK 有两种方式：
- 方式一： 在项目需要使用 SDK API 的文件里，添加模块引用。
```
@import TXLiteAVSDK_International;
```

- 方式二：在项目需要使用 SDK API 的文件里，引入具体的头文件。
```
#import <TXLiteAVSDK.h>
```

## 给 SDK 配置 License 授权

单击 [License 申请](https://console.cloud.tencent.com/live/license) 获取测试用 License，您会获得两个字符串：一个字符串是 licenseURL，另一个字符串是解密 key。

在您的 App 调用 LiteAVSDK 的相关功能之前（建议在 `- [AppDelegate application:didFinishLaunchingWithOptions:]` 中）进行如下设置：

```objc
@import TXLiteAVSDK_Professional;
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
### LiteAVSDK 是否支持后台运行？
支持，如需要进入后台仍然运行相关功能，可选中当前工程项目，在 **Capabilities** 下设置  **Background Modes** 为 **ON**，并勾选 **Audio，AirPlay and Picture in Picture** ，如下图所示：
![](https://main.qcloudimg.com/raw/9c8698d4fc563b7d0d70f415b7471572.png)


