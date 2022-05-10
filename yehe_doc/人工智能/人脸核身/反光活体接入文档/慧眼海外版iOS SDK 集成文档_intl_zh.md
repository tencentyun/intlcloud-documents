### 一、开发准备

1. 注册腾讯云账号，点击进入慧眼控制台，即可开通相应服务。
2. 从慧眼SDK下载链接中下载SDK，并集成到本地。
3. 申请获取License文件



### 二、iOS端慧眼 SDK接入流程

#### 1. 依赖环境

1. 开发环境 Xcode 11.0 或以上

2. 慧眼iOS SDK 适用于手机iOS 9.0及以上版本

   

#### 2. 手动接入方式

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



#### 3. 使用Pod方式接入

1. 将CloudHuiYanSDK_FW文件夹复制到集成项目Podfile同级目录下

   

2. 在Podfile设置

```ruby
target 'HuiYanAuthDemo' do
  use_frameworks! 
  pod 'CloudHuiYanSDK_FW', :path => './CloudHuiYanSDK_FW'
end
```

3. pod install 更新

>Tips：注意CloudHuiYanSDK_FW.podspec 里面 vendored_frameworks 与 resource 设置的相对位置，可根据实际SDK目录位置修改



#### 3. Build Phases设置

1. Other Linker Flags 新增 **-ObjC**
2. 接入ViewController.m 设置后缀为.mm



#### 4. 权限设置

SDK需要手机网络及 摄像头使用权限，请添加对应的权限声明。在主项目info.plist 配置中添加下面key-value值

```xml
<key>Privacy - Camera Usage Description</key>
<string>人脸核身需要开启您的摄像头权限，用于人脸识别</string>
```



#### 5. 整体流程图

下图展示了SDK、客户端以及服务器端的整体交互逻辑。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





#### 6. SDK接口调用使用说明

##### 6.1 初始化配置，并拉取配置参数

在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息用来兑换光线序列，大概流程如下：

1. 设置SDK配置信息**HuiYanOsConfig** （设置lic文件路径，本地检测超时时间，是否清除本地视频缓存等）

2. 调用**startGetAuthConfigData:**获取本地配置参数**result**

3. 将上一步获取的本地参数信息，通过调用云API接口**GenerateReflectSequence**获取光线序列

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
  	NSString *reflectSequence = [self getLiveDataWith:result];
} withFailCallback:^(int errCode, NSString * _Nonnull errMsg) {
  	// 获取配置参数失败（客户自己实现）
    NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```



##### 6.2 完成剩余步骤活体核身

	当您已经将配置信息从服务器端兑换完成之后，将服务器下发的**reflectSequence**也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能，大致流程如下：

1. 调用**startAuthByLightData:**传入**reflectSequence**进入SDK活体检测页面

2. 完成活体检测**SuccCallback**返回结果**data**

3. 最后将核身数据**data**通过调用云API接口**DetectReflectLivenessAndCompare**进行核身比对，获得最终比对结果

```objective-c
[HuiYanOsApi startAuthByLightData:reflectSequence withSuccCallback:^(NSData * _Nonnull data, NSString * _Nonnull videoPath) {
     	//活体通过检测结果数据
  		// 1. 将本地核身的数据信息，发送到服务器端做比对验证，得到最终结果。（客户自己实现）
		 	[self checkAuthResultByData:data];
			// 2. 处理本地核身视频videoPath。（客户自己实现）
			[self dealWithAuthVideo:videoPath];
} withFailCallback:^(int errCode, NSString * _Nonnull errMsg) {
  		// 本地核身失败获取，发生错误
      NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

>**tips** ：当getLightData出现异常时，需要退出SDK，则可以调用 [HuiYanOsApi startAuthByLightData:nil withSuccCallback:nil withFailCallback:nil] 方法结束当前SDK会话。在startGetAuthConfigData中FailCallback返回错误回调。



##### 6.3 SDK资源释放

	在您APP退出使用的时候，可以调用SDK资源释放接口

```objective-c
// 退出时做资源释放
- (void)dealloc {
    [HuiYanOsApi release];
}
```



### 三、常见错误

1. **errCode:210, errMsg:HuiYanOsConfig param error** ：检查license文件路径是否设置和设置是否正确，是否填加至 **Copy Bundle Resource**

2. **[HuiYanOsApi startAuthByLightData:@"" withSuccCallback:nil withFailCallback:nil];** 返回**errCode:215, errMsg:User voluntarily Stop** 主动停止SDK验证

3. **errCode:210, errMsg:lightData is err** lightData光线数据格式错误
4. Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '\**\* -[__NSDictionaryM setObject:forKey:]: key cannot be nil'  处理方法 **Other Linker Flags 新增 -ObjC**
