



### 开发准备

1. 注册腾讯云账号，点击进入慧眼控制台，即可开通相应服务。
2. 从慧眼SDK下载链接中下载SDK，并集成到本地。
3. 申请获取License文件

### iOS端慧眼 SDK接入流程

#### 依赖环境

1. 开发环境 Xcode 11.0 或以上
2. 慧眼iOS SDK 适用于手机iOS9.0及以上版本

#### **1.手动接入方式**

1. 导入相关库及文件

Link Binary With Libraries导入相关Framework

2. SDK依赖的库如下

```
├──HuiYanSDK.framework
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
├── libc++.tbd
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

#### 2.使用Pod方式接入

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

#### Build Phases设置

1. Other Linker Flags 新增 **-ObjC**
2. 接入ViewController.m 设置后缀为.mm(swift 工程添加系统库libc++.tbd)

#### 权限设置

SDK需要手机网络及 摄像头使用权限，请添加对应的权限声明。在主项目info.plist 配置中添加下面key-value值

```xml
<key>Privacy - Camera Usage Description</key>
<string>人脸核身需要开启您的摄像头权限，用于人脸识别</string>
```



## 深度接入流程

#### 整体流程图

下图展示了SDK、客户端以及服务器端的整体交互逻辑。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan_overseas/image/clipboard_20210412_035342.png)



#### SDK接口使用说明

##### 初始化配置，并拉取配置参数

在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息

```objective-c
// HuiYanOs的相关参数
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
// license文件在bundle中的路径
config.authLicense = [[NSBundle mainBundle] pathForResource:@"YTFaceSDK.license" ofType:@""];
// 活体检测本地检测超时时间（ms）
config.authTimeOutMs = 20000;
//指定HuiYanSDKUI.bundle 内语言目录文件
config.setLanguageFileName = @"th";//th.lproj
// 启动核身前，拉取本地的配置参数信息
[HuiYanOsApi startGetAuthConfigData:config withSuccCallback:^(NSString * _Nonnull result) {
  	// 获取配置信息成功, 将配置信息发送给服务器，兑换启动核身配置，服务器下发的光线序列（客户自己实现）
  	NSString *liveData = [self getLiveDataWith:result];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
  	// 获取配置参数失败（客户自己实现）
    NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

##### 完成剩余步骤活体核身

​	当您已经将配置信息从服务器端兑换完成之后，将服务器下发的LightData也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能。

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

> **tips** ：当getLightData出现异常时，需要退出SDK，则可以调用 [HuiYanOsApi startAuthByLightData:nil withSuccCallback:nil withFialCallback:nil] 方法结束当前SDK会话。在startGetAuthConfigData中FialCallback返回错误回调。
>
> swift 项目可调用HuiYanOsApi.stopAuth

##### SDK资源释放

​	在您APP退出使用的时候，可以调用SDK资源释放接口

```objective-c
// 退出时做资源释放
- (void)dealloc {
    [HuiYanOsApi release];
}
```

### API的详细说明

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigCallback以及HuiYanResultCallBack。

#### HuiYanOsApi

| API                                                   | 功能描述                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release())                               | 资源释放接口                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口                        |
| [startAuthByLightData()](#startAuthByLightData())     | 传入服务器获取的光线序列，继续完成活体核身检测的接口 |



#### release()

```objective-c
+ (void)release;
```

功能介绍：

​	慧眼SDK资源释放的接口。

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
              withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
              withFialCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

功能介绍：

​	本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型                                              | 参数名称                 | 参数含义               |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig)                     | huiYanOsConfig           | 配置的参数             |
| [HuiYanConfigSuccCallback](#HuiYanConfigSuccCallback) | huiYanConfigSuccCallback | 拉取配置结果成功的回调 |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | 拉取配置结果失败的回调 |



#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)lightData
         withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
         withFialCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

功能介绍：

​	将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型                                              | 参数名称                 | 参数含义                                   |
| ----------------------------------------------------- | ------------------------ | ------------------------------------------ |
| NSString                                              | lightData                | 从服务器兑换来启动核身使用的光线序列Base64 |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | 本地核身的结果成功回调                     |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | 本地核身的结果失败回调                     |



#### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型                          | 名称                   | 含义                                                         | 默认值            |
| ----------------------------- | ---------------------- | ------------------------------------------------------------ | ----------------- |
| NSString                      | authLicense            | 客户申请的用户核审授权的Licens文件名                         | 空                |
| long | authTimeOutMs|设置活体检测的超时时间 | 10000毫秒（10秒） |
| long | prepareTimeoutMs|设置准备阶段检测的超时时间 | 0 |
| [HYShowTimeOutMode](#HYShowTimeOutMode) | showTimeOutMode|设置显示倒计时阶段 | HYShowTimeOutMode_PREPARE|HYShowTimeOutMode_ACTION |
| BOOL                          | isDeleteVideoCache     | 是否删除核身视频的本地缓存                                   | YES               |
| BOOL                          | iShowTipsPage          | 是否显示引导页                                               | NO                |
| NSString | userUIBundleName| 自定义的UI的bundle文件名 比如 UserUIBundle.bundle 则设置为"UserUIBundle"; | nil |
| NSString | userLanguageFileName   | 自定义的languageBundle 名称 比如 UseLanguage.bundle 则设置为"UseLanguage"; | nil               |
| NSString | userLanguageBundleName | 自定义本地国际化文件名 比如 en.lproj 则设置为"en";           | nil               |
| [LanguageType](#LanguageType) | languageType           | SDK内部文字语言设置                                          | DEFAULT           |
| BOOL                          | isGetBestImg           | 精简模式下是否获取最佳帧图片                             | NO               |
| NSString | setLanguageFileName | 默认HuiYanSDKUI.bundle 内新增的语言文件目录名称 优先级最高 | nil |
#### HuiYanConfigSuccCallback

初始化并且获取本地配置成功的回调

```objective-c
/**
 * 初始化成功回调
 *
 * @param result 初始化回调数据
 */
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

#### HuiYanConfigFailCallback

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



#### HuiYanResultSuccCallback

本地核身流程与本地结果获取成功的回调

```objective-c
/**
 * 活体核身成功回调
 *
 * @param data 活体比对数据，GZip压缩后的数据
 * @param videoPath 活体视频路径
 */
typedef void (^HuiYanResultSuccCallback)(NSData * _Nonnull data, NSString * _Nonnull videoPath);
```

#### HuiYanResultFailCallback

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

#### LanguageType 

SDK内包含的国际化String

```objective-c
typedef enum : NSUInteger {
    DEFAULT = 0,//跟随系统设置
    ZH_HANS,//中文简体
    ZH_HANT,//中文繁体
    ZH_HK,//中文繁体香港
    ZH_TW,//中文繁体台湾
    EN,//英文
    MS,//马来西亚语
    RU,//俄语
    JA,//日语
    CUSTOMIZE_LANGUAGE, //定制语言
} LanguageType;
```

#### HYShowTimeOutMode
```objective-c
typedef NS_OPTIONS(int, HYShowTimeOutMode) {
    HYShowTimeOutMode_TIMEOUT_HIDDEN = 1 << 0,// 隐藏所有倒计时
    HYShowTimeOutMode_PREPARE = 1 << 1,// 准备阶段倒计时
    HYShowTimeOutMode_ACTION = 1 << 3,// 动作阶段倒计时
};
```

## 精简版接入流程

当前版本包含与后端接口交互，获取token来开启验证流程

1. 服务端接口获取验证token
2. 开启慧眼SDK进入核身页面
3. 核身结束处理最佳帧（如有）
4. 通过token获取核身结果

整体流程图

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan_overseas/image/huiyan_overseas_2.png)

#### SDK接口使用说明
开启慧眼SDK活体检测流程

```objective-c
#import <HuiYanSDK/HuiYanOsApi.h>
#import <HuiYanSDK/HuiYanOSKit.h>

  //获取token
    NSString *faceToken = self.tokenTextField.text;
    // 配置SDK
    HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
    //设置lic
    config.authLicense = [[NSBundle mainBundle] pathForResource:@"xxx.lic" ofType:@""];
    //准备阶段超时配置
    config.prepareTimeoutMs = 20000;
    //检测阶段超时配置
    config.authTimeOutMs = 20000;
    config.isDeleteVideoCache = YES;
    config.languageType = EN;
    //    config.userLanguageFileName = @"ko";
    //    config.userLanguageBundleName = @"UseLanguageBundle";
    config.iShowTipsPage = YES;
    config.isGetBestImg = YES;

    [[HuiYanOSKit sharedInstance] startHuiYaneKYC:faceToken withConfig:config
                                  witSuccCallback:^(HuiYanOsAuthResult * _Nonnull authResult, id  _Nullable reserved) {
        NSString *bestImg = authResult.bestImage;
        NSString *token = authResult.faceToken;
        
    } withFailCallback:^(int errCode, NSString * _Nonnull errMsg, id  _Nullable reserved) {
        NSString *showMsg = [NSString stringWithFormat:@"err:%d:%@",errCode,errMsg];
        NSLog(@"err:%@",showMsg);
    }];
```



### API的详细说明

精简版接入慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOSKit， 参数配置类HuiYanOsConfig，结果回调类HuiYanOKitSuccCallback以及HuiYanOKitFailCallback。

#### HuiYanOSKit
| API                                   | 功能描述                |
| ------------------------------------- | ----------------------- |
| [startHuiYaneKYC()](#startHuiYaneKYC) | 进入慧眼SDK活体检测流程 |
| [sdkVersion()](#release())            | 获取sdk版本号           |

#### startHuiYaneKYC

功能介绍：

​	开启活体检测SDK，并配置SDK，回调返回结果或错误

```objective-c
/// 开启慧眼活体检测流程
/// @param faceToken token
/// @param kitConfig SDK配置
/// @param succCallback 活体检测成功回调
/// @param failCallback 活体检测失败回调
- (void)startHuiYaneKYC:(NSString *)faceToken withConfig:(HuiYanOsConfig *)kitConfig
        witSuccCallback:(HuiYanOKitSuccCallback)succCallback
       withFailCallback:(HuiYanOKitFailCallback)failCallback;
```

传入参数：

| 数类型                                            | 参数名称     | 参数含义         |
| ------------------------------------------------- | ------------ | ---------------- |
| NSSting                                           | faceToken    | 活体流程单号     |
| [HuiYanOsConfig](#HuiYanOsConfig)                 | kitConfig    | SDK配置类        |
| [HuiYanOKitSuccCallback](#HuiYanOKitSuccCallback) | succCallback | 活体检测成功回调 |
| [HuiYanOKitFailCallback](#HuiYanOKitFailCallback) | failCallback | 活体检测失败回调 |

#### HuiYanOsAuthResult

| 数类型  | 参数名称  | 参数含义                                       |
| ------- | --------- | ---------------------------------------------- |
| NSSting | faceToken | 活体流程token                                  |
| NSSting | bestImage | 开启最佳桢返回时，成功后返回的最佳桢base64图片 |

#### HuiYanOKitSuccCallback

```objective-c
/**
 * 活体检测成功回调
 *
 * @param authResult  活体验证结果
 * @param reserved 预留位
 */
typedef void (^HuiYanOKitSuccCallback)(HuiYanOsAuthResult * _Nonnull authResult, id _Nullable reserved);
```

#### HuiYanOKitFailCallback

```objective-c
/**
 * 活体检测失败回调
 *
 * @param errCode 错误码
 * @param errMsg 错误信息
 * @param reserved 预留位
 */
typedef void (^HuiYanOKitFailCallback)(int errCode, NSString * _Nonnull errMsg ,id _Nullable reserved);
```



##SDK终端错误码(iOS)

```
    HY_SUCCESS                              = 0,
    // 初始化参数异常
    HY_INITIALIZATION_PARAMETER_EXCEPTION   = 210,
    // bundle配置异常
    HY_BUNDLE_CONFIGURATION_EXCEPTION       = 211,
    // 优图配置异常
    HY_YTSDK_CONFIGURATION_EXCEPTION        = 212,
    // 先调用初始化接口
    HY_PLEASE_CALL_FIRST_INIT_API           = 213,
    // SDK 授权失败
    HY_SDK_AUTH_FAILED                      = 214,
    // 用户手动取消
    HY_USER_VOLUNTARILY_CANCELED            = 215,
    // SDK 人脸本地检测失败
    HY_YTSDK_LOCAL_AUTH_FAILED              = 216,
    // 相机开启失败
    HY_CAMERA_OPEN_FAIL                     = 217,
    // 请勿在核身过程中切换应用
    HY_DONOT_SWITCH_APPS                    = 218,
    // 摄像头权限异常
    HY_CAMEREA_PERMISSION_EXCEPTION         = 219,
    // 视频裁剪失败
    HY_SDK_VEDIO_CUT_EXCEPTION              = 220,
    // 光线数据格式错误
    HY_LIGHT_DATA_FORMAT_EXCEPTION          = 221
```



## 设置自定义SDK语言

1.将自定义UseLanguage.bundle添加至项目中(Copy Bundle Resources)



![image_1](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/iOS%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/huiyan/img_10.png)

2.配置设置如下

```
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.languageType = CUSTOMIZE_LANGUAGE; 
config.userLanguageFileName = @"ko";//例：设置 ko.lproj 
config.userLanguageBundleName = @"UseLanguage";//自定义打包bundle名称 例： UseLanguage.bundle
```

若config.languageType = DEFAULT;则会从自定义Bundle找该地区的语言文件，若是未找到则默认为en。



## 设置自定义UI

### 1、自定义UI

1）图标Icon。可以将Icon替换到以下列表，命名要保持原有命名。

![image-20230110144933817](https://qcloudimg.tencent-cloud.cn/raw/ca4171a7a422b149bf6f2908f9608b8d.png)

2）xib内布局调整。如TXYOsAuthingViewController 识别页面，可以修改xib内组件的布局，增加静态组件，但是不允许删除组件。该页面逻辑由SDK内部.m文件完成，仅支持修改布局和增加无逻辑组件（如增加背景图）。

![image-20230110145052550](https://qcloudimg.tencent-cloud.cn/raw/4f588059f114b5e8ff598e66bcc81025.png)

3）通过设置userUIBundleName字段设置到SDK中
```object-c
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.userUIBundleName = @"UserUIBundle"
```

