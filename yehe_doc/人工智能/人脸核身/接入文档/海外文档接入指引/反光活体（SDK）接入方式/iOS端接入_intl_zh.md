### 依赖环境

1. 开发环境 Xcode 11.0 或以上
2. 慧眼iOS SDK 适用于手机iOS9.0及以上版本

### **1.手动接入方式**

1. 导入相关库及文件

Link Binary With Libraries导入相关Framework

2. SDK依赖的库如下

```
├──HuiYanSDK.framework
├──TXYComm.framework
├──YtSDKKitSilentLiveness.framework
├──YtSDKKitReflectLiveness.framework
├──YtSDKKitActionLiveness.framework
├──YtSDKKitFramework.framework
├──tnnliveness.framework
├──YTFaceAlignmentTinyLiveness.framework
├──YTFaceTrackerLiveness.framework
├──YTFaceDetectorLiveness.framework
├──YTPoseDetector.framework
├──YTCommonLiveness.framework
└──YTFaceLiveReflect.framework
```

3. Link Binary With Libraries导入系统Framework

```
├── AVFoundation.framework
└── Accelerate.framework
```

4. Copy Bundle Resources中导入模型

```
└── face-tracker-v001.bundle
```

5. Copy Bundle Resources导入资源文件

```
└── HuiYanSDKUI.bundle
```

### 2.使用Pod方式接入

1. 将CloudHuiYanSDK_FW文件夹复制到集成项目Podfile同级目录下
2. 在Podfile设置

```ruby
target 'HuiYanAuthDemo' do
use_frameworks! 
pod 'CloudHuiYanSDK_FW', :path => './CloudHuiYanSDK_FW'
end
```

3. pod install 更新

>文件层级和具体的设置可以参考Demo

### Build Phases设置

1. Other Linker Flags 新增 **-ObjC**
2. 接入ViewController.m 设置后缀为.mm
3. Enable BitCode 设置 NO

### 权限设置

SDK需要手机网络及 摄像头使用权限，请添加对应的权限声明。在主项目info.plist 配置中添加下面key-value值

```xml
<key>Privacy - Camera Usage Description</key>
<string>人脸核身需要开启您的摄像头权限，用于人类识别</string>
```


### SDK接口使用说明

#### 初始化配置，并拉取配置参数

在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息

```objective-c
// HuiYanOs的相关参数
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
// license文件在bundle中的路径
config.authLicense = [[NSBundle mainBundle] pathForResource:@"YTFaceSDK.license" ofType:@""];
// 活体检测本地检测超时时间（ms）
config.authTimeOutMs = 20000;
// 启动核身前，拉取本地的配置参数信息
[HuiYanOsApi startGetAuthConfigData:config withSuccCallback:^(NSString * _Nonnull result) {
// 获取配置信息成功, 将配置信息发送给服务器，兑换启动核身配置，服务器下发的光线序列（客户自己实现）
NSString *liveData = [self getLiveDataWith:result];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
// 获取配置参数失败（客户自己实现）
NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

#### 完成剩余步骤活体核身

当您已经将配置信息从服务器端兑换完成之后，将服务器下发的LightData也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能。

```objective-c
[HuiYanOsApi startAuthByLightData:liveData withSuccCallback:^(NSData * _Nonnull data, NSString * _Nonnull videoPath) {
//活体通过检测结果数据
// 1. 将本地核身的数据信息，发送到服务器端做比对验证，得到最终结果。（客户自己实现）
[self checkAuthResultByData:data];
// 2. 处理本地核身视频videoPath。（客户自己实现）
[self dealWithAuthVideo:videoPath];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
// 本地核身失败获取，发生错误
NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

#### SDK资源释放

在您APP退出使用的时候，可以调用SDK资源释放接口

```objective-c
// 退出时做资源释放
- (void)dealloc {
[HuiYanOsApi release];
}
```


## IOS API的详细说明

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigCallback以及HuiYanResultCallBack。

### HuiYanOsApi

| API | 功能描述 |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release()) | 资源释放接口 |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口 |
| [startAuthByLightData()](#startAuthByLightData()) | 传入服务器获取的光线序列，继续完成活体核身检测的接口 |


#### release()

```objective-c
+ (void)release;
```

功能介绍：

慧眼SDK资源释放的接口。

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
withFialCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

功能介绍：

本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型 | 参数名称 | 参数含义 |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig) | huiYanOsConfig | 配置的参数 |
| [HuiYanConfigSuccCallback](#HuiYanConfigSuccCallback) | huiYanConfigSuccCallback | 拉取配置结果成功的回调 |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | 拉取配置结果失败的回调 |


#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)lightData
withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
withFialCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

功能介绍：

将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型 | 参数名称 | 参数含义 |
| ----------------------------------------------------- | ------------------------ | ------------------------------------ |
| NSString | lightData | 从服务器兑换来启动核身使用的光线序列 |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | 本地核身的结果成功回调 |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | 本地核身的结果失败回调 |


### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型 | 名称 | 含义 | 默认值 |
| --------- | ------------------ | ------------------------------------ | ----------------- |
| NSSString | authLicense | 客户申请的用户核审授权的Licens文件名 | 空 |
| long | authTimeOutMs | 设置活体检测的超时时间 | 10000毫秒（10秒） |
| BOOL | isDeleteVideoCache | 是否删除核身视频的本地缓存 | YES |

### HuiYanConfigSuccCallback

初始化并且获取本地配置成功的回调

```java
/**
* 初始化成功回调
*
* @param result 初始化回调数据
*/
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

### HuiYanConfigFailCallback

初始化并且获取本地配置失败的回调

```objective-c
/**
* 初始化失败回调
*
* @param errCode 错误码
* @param errMsg 错误信息
*/
typedef void (^HuiYanConfigFailCallback)(int errCode, NSString * _Nonnull errMsg);
```


### HuiYanResultSuccCallback

本地核身流程与本地结果获取成功的回调

```objective-c
/**
* 活体核身成功回调
*
* @param data 活体二进制比对数据，压缩后的数据
* @param videoPath 活体视频路径
*/
typedef void (^HuiYanResultSuccCallback)(NSString * _Nonnull data, NSString * _Nonnull videoPath);
```

### HuiYanResultFailCallback

本地核身流程与本地结果获取失败的回调

```objective-c
/**
* 活体核身失败回调
*
* @param errCode 错误码
* @param errMsg 错误信息
*/
typedef void (^HuiYanResultFailCallback)(int errCode, NSString * _Nonnull errMsg);
```