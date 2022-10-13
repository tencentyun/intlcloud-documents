#摄像头推流Intl

[原文地址](https://github.com/tencentyun/qcloud-documents/edit/master/product/%E8%A7%86%E9%A2%91%E6%9C%8D%E5%8A%A1/%E7%A7%BB%E5%8A%A8%E7%9B%B4%E6%92%AD/%E5%9F%BA%E7%A1%80%E5%8A%9F%E8%83%BD/%E6%91%84%E5%83%8F%E5%A4%B4%E6%8E%A8%E6%B5%81/iOS.md)

## 功能概述
摄像头推流，是指采集手机摄像头的画面以及麦克风的声音，进行编码之后再推送到直播云平台上。腾讯云 LiteAVSDK 通过 TXLivePusherV2 接口提供摄像头推流能力。
![](https://main.qcloudimg.com/raw/f4df6e007076f4629629f5d75f14d86d.png)


## 特别说明

- **x86 模拟器调试**
由于 SDK 大量使用 iOS 系统的音视频接口，这些接口在 Mac 上自带的 x86 仿真模拟器下往往不能工作。所以，如果条件允许，推荐您尽量使用真机调试。


## 功能对接

### 1. 下载 SDK 开发包
/// TODO URL下载地址替换
[下载](https://intl.cloud.tencent.com/document/product/1071/38150) SDK 开发包，并按照 [SDK 集成指引](https://intl.cloud.tencent.com/document/product/1071/38155) 将 SDK 嵌入您的 App 工程中。

<span id="step2"></span>
### 2. 给 SDK 配置 License 授权
单击 [License 申请](https://console.cloud.tencent.com/live/license) 获取测试用的 License，您会获得两个字符串：一个字符串是 licenseURL，另一个字符串是解密 key。

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

### 3. 初始化 TXLivePusherV2 组件
首先创建一个`TXLivePusherV2`实例。后续所有推流相关的能力包括开启/停止推流，开启/停止摄像头采集，开启/停止声音采集，开启/停止耳返，音质，画质设置都可通过该实例来实现。

```objectivec    
 TXLivePusherV2 *_pusher = [[TXLivePusherV2 alloc] init];
 [_pusher setObserver:self];
```

### 4. 开启摄像头预览
/// TODO 接口文档地址替换
调用 TXLivePusherV2 中的`setRenderView`接口可以开启当前手机的摄像头预览。您需要为`setRenderView` 接口提供一个用于显示预览画面的 view 对象。

```objectivec   
 //创建一个 view 对象，并将其嵌入到当前界面中
 UIView *localView = [[UIView alloc] initWithFrame:self.view.bounds];
 [self.view insertSubview:localView atIndex:0];
 localView.center = self.view.center;
 
 //启动本地摄像头预览
 [_pusher setRenderView:localView];
```

> ! 如果要给 view 增加动画效果，需要修改 view 的 transform 属性而不是 frame 属性。
```objectivec
  [UIView animateWithDuration:0.5 animations:^{
      _localView.transform = CGAffineTransformMakeScale(0.3, 0.3); //缩小1/3
  }];
```

### 5. 启动和结束推流
如果已经通过`setRenderView`接口启动了摄像头预览，就可以调用 TXLivePusherV2 中的`startPush`接口开始推流。

```objectivec 
//启动推流
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx"; //此处填写您的 rtmp 推流地址
[_pusher startPush:rtmpUrl];
[_pusher startCamera]; // 开启摄像头采集
[_pusher startMicrophone]; // 开启麦克风采集
```

推流结束后，可以调用 TXLivePusherV2 中的`stopPush`接口结束推流。
```objectivec
//结束推流
[_pusher setObserver:nil];
[_pusher stopCamera];
[_pusher stopMicrophone];
[_pusher stopPush];
```

-  **如何获取可用的推流 URL？**

开通直播服务后，可以使用【直播控制台】>【辅助工具】> [【地址生成器】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) 生成推流地址。
![](https://main.qcloudimg.com/raw/0ec9d83f340454c287d96f83eec3a3e4.png)

- **返回 -5 的原因？**
如果 `startPush` 接口返回 -5，则代表您的 License 校验失败了，请检查 [第2步“给 SDK 配置   License 授权”](#step2) 中的工作是否有问题。


### 6. 纯音频推流
如果您的直播场景是纯音频直播，不需要视频画面，那么您可以执行：
```objectivec 
//启动推流
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx"; //此处填写您的 rtmp 推流地址
[_pusher startPush:rtmpUrl];
[_pusher startMicrophone]; // 开启麦克风采集
```

### 7. 设定画面清晰度
调用 TXLivePusherV2 中的`setVideoQuality:resolutionMode:`接口，可以设定观众端的画面清晰度、高宽比、横竖屏模式。

```objectivec
// 竖屏1280x720，第一个参数为清晰度，第二个参数为横竖屏模式
[_pusher setVideoQuality:TXLiveVideoResolution_1280x720 resolutionMode:TXLiveVideoResolutionMode_Portrait];
```

### 8. 美颜美白和红润特效
/// TODO 美颜需要使用到美颜SDK
美颜可以通过引入美颜SDK（TCBeautyPanel.framework），传入 `TXLivePusherV2 `实例对象，并在界面上展示美颜面板（TCBeautyPanel）即可实现丰富的美颜特效。
```objectivec
NSUInteger controlHeight = [TCBeautyPanel getHeight];
CGRect frame = CGRectMake(0, 0, self.view.frame.size.width, controlHeight);
_beautyPanel = [TCBeautyPanel beautyPanelWithFrame:frame
                                         SDKObject:_livePusher];
[ThemeConfigurator configBeautyPanelTheme:_beautyPanel];
_beautyPanel.pituDelegate = self; // 设置并实现美颜的代理方法
[_beautyPanel resetAndApplyValues];

#pragma mark - BeautyLoadPituDelegate

- (void)onLoadPituStart {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showInProgressText:@"开始加载资源"];
    });
}

- (void)onLoadPituProgress:(CGFloat)progress {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showInProgressText:[NSString stringWithFormat:@"正在加载资源%d %%",(int)(progress * 100)]];
    });
}

- (void)onLoadPituFinished {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showText:@"资源加载成功"];
    });
}

- (void)onLoadPituFailed {
    dispatch_async(dispatch_get_main_queue(), ^{
        [self showText:@"资源加载失败"];
    });
}
```


### 9. 控制摄像头
TXLivePusherV2 提供了一个 API 获取相机设备管理对象TXVideoDeviceManager 用于控制摄像头的行为：

| API 函数 | 功能说明 | 备注说明 |
|---------|---------|---------|
| switchCamera | 切换前后摄像头 | Mac 平台对应的函数为 `selectCamera`。 |
| enableCameraFlash | 打开或关闭闪光灯 | 仅在当前是后置摄像头时有效。|
| setCameraZoomRatio | 调整摄像头的焦距 | 焦距大小，取值范围：1 - 5，默认值建议设置为1即可。|
| setCameraFocusPosition | 设置手动对焦位置 | 需要可以通过enableCameraAutoFocus设置关闭自动对焦|

### 10. 观众端的镜像效果
调用 TXLivePusherV2 中的`setEncoderMirror`接口可以设置观众端的镜像效果。之所以说是观众端的镜像效果，是因为当主播在使用前置摄像头直播时，自己看到的画面会被 SDK 默认反转，这时主播的体验跟自己照镜子时的体验是保持一致的。`setEncoderMirror`所影响的是观众端观看到的画面情况，如下图所示：
/// TODO 图片替换
![](https://main.qcloudimg.com/raw/4d3c88bb408559800fe87e277d180b99.png)

### 11. 设置音质
```objectivec
// 请注意调用顺序：
[_pusher setAudioQuality: TXLiveAudiOQuality_Music]; // 1 音频质量设置，必须在开始推流之前设置才会生效
[_pusher startPush]; // 2
```

### 12. 背景音乐、变声、混响

// TODO 混音组件介绍链接

支持使用[混音组件AudioEffectSettingKit.framework](/// TODO 混音组件介绍链接)设置背景音乐、变声、混响。
a.背景音乐：主播通过混音组件见面板，背景音乐，选择背景音乐，完成后，观众即可收听到主播选择的背景音乐。
b.变声：主播通过混音组件面板，变声，选择变声类型，完成后，观众端收听到的主播声音将变为对应的变声。
c.混响：主播通过混音组见面板，混响，选择混响类型，完成后，观众端即可收听到对应混响。
以上三种方式可以同时使用，效果叠加，玩法更加多样。
使用方式：

```objectivec
    /// BGM 控件设置
- (void)setUpAudioSettingUI {
    /// 1.初始化混音组件
    _audioEffectView = [[AudioEffectSettingView alloc] initWithType:AudioEffectSettingViewDefault];
    _audioEffectView.delegate = self;
    _audioEffectView.backgroundColor = [UIColor.blackColor colorWithAlphaComponent:0.8];
    _audioEffectView.alpha = 1.0;
    _audioEffectView.hidden = NO;

    /// 2.关联混音组件与推流器
    [_audioEffectView setAudioEffectManager:_livePusher.getAudioEffectManager];
}
```
效果图：
![](https://main.qcloudimg.com/raw/5b1bc5b6e1a8aada3af7b1ebe70ab108.jpg)

### 13. 设置 Logo 水印

通过 TXLivePusherV2 中的`setWatermark:position:scale:`可以让 SDK 在推出的视频流中增加一个水印，水印位置位是由`position`参数决定。

- SDK 所要求的水印图片格式为 png 而不是 jpg，因为 png 这种图片格式有透明度信息，因而能够更好地处理锯齿等问题（将 jpg 图片在 Windows 下修改后缀名是不起作用的）。
- `position`设置的是水印图片相对于推流分辨率的归一化坐标。假设推流分辨率为：540 × 960，该字段设置为：（0.1，0.1，0.1，0.0），那么水印的实际像素坐标为：（540 × 0.1，960 × 0.1，水印宽度 × 0.1，水印高度会被自动计算）。

```objectivec
UIImage *image = value?[UIImage imageNamed:@"watermark"]:nil;
CGPoint pos = value?CGPointMake(10, 10):CGPointZero;
[_pusher setWatermark:image position:pos scale:1.0];
```

### 14. 发送 SEI 消息 
调用 TXLivePusherV2 中的 `sendSEIMessage`接口可以发送 SEI 消息。所谓 SEI，是视频编码数据中规定的一种附加增强信息，平时一般不被使用，但我们可以在其中加入一些自定义消息，这些消息会被直播 CDN 转发到观众端。使用场景有：

1. 答题直播：推流端将**题目**下发到观众端，可以做到“音-画-题”完美同步。
2. 秀场直播：推流端将**歌词**下发到观众端，可以在播放端实时绘制出歌词特效，因而不受视频编码的降质影响。
3. 在线教育：推流端将**激光笔**和**涂鸦**操作下发到观众端，可以在播放端实时地划圈划线。

由于自定义消息是直接被塞入视频数据中的，所以不能太大（几个字节比较合适），一般常用于塞入自定义的时间戳等信息。

```objectiveC
NSString* msg = @"test";
[_pusher sendSEIMessage:[msg dataUsingEncoding:NSUTF8StringEncoding]];
```

常规开源播放器或者网页播放器是不能解析 SEI 消息的，必须使用 LiteAVSDK 中自带的 TXLivePlayerV2 才能解析这些消息：

当 TXLivePlayerV2 所播放的视频流中有 SEI 消息时，会通过 TXLivePlayerObserver 中的 **onRecvSEIMessage**通知给您。

## 事件处理
### 1. 事件监听

// TODO 接口文档链接需要更换

SDK 通过 TXLivePusherObserver 代理来设置推流器回调，通过设置回调，可以监听 TXLivePusherV2 推流器的一些回调事件，包括推流器状态、音量回调、统计数据、警告和错误信息等。

### 2. 常规事件 
一次成功的推流都会通知的事件有（例如，收到0就意味着此次事件调用成功了）：

| 事件 ID                 |    数值  |  含义说明                    |
| :-------------------  |:-------- |  :------------------------ |
|TXLIVE_OK            | 0 | 此次推流事件调用成功 |

### 3. 错误通知 
SDK 发现部分严重问题，推流无法继续（例如，用户禁用了 App 的 Camera 权限导致摄像头打不开）：

| 事件 ID                 |    数值  |  含义说明                    |
| :-------------------  |:-------- |  :------------------------ |
| TXLIVE_ERROR_FAILED                   | -1    | 失败错误。                                                   |
| TXLIVE_ERROR_INVALID_PARAMETER        | -2    | 非法参数错误。                                               |
| TXLIVE_ERROR_REFUSED                  | -3    | 拒绝错误。                                                   |
| TXLIVE_ERROR_NOT_SUPPORTED            | -4    | 不被支持错误。                                               |
| TXLIVE_ERROR_INVALID_LICENSE          | -5    | 非法许可错误。                                               |
| TXLIVE_ERROR_CAMERA_START_FAILED      | -1301 | 打开摄像头失败，例如在 Windows 或 Mac 设备，摄像头的配置程序（驱动程序）异常，禁用后重新启用设备，或者重启机器，或者更新配置程序。 |
| TXLIVE_ERROR_CAMERA_OCCUPIED          | -1316 | 摄像头正在被占用中，可尝试打开其他摄像头。                   |
| TXLIVE_ERROR_CAMERA_NO_PERMISSION     | -1314 | 摄像头设备未授权，通常在移动设备出现，可能是权限被用户拒绝了。 |
| TXLIVE_ERROR_MICROPHONE_START_FAILED  | -1302 | 打开麦克风失败，例如在 Windows 或 Mac 设备，麦克风的配置程序（驱动程序）异常，禁用后重新启用设备，或者重启机器，或者更新配置程序。 |
| TXLIVE_ERROR_MICROPHONE_OCCUPIED      | -1319 | 麦克风正在被占用中，例如移动设备正在通话时，打开麦克风会失败。 |
| TXLIVE_ERROR_MICROPHONE_NO_PERMISSION | -1317 | 麦克风设备未授权，通常在移动设备出现，可能是权限被用户拒绝了。 |

### 4. 警告事件 
SDK 发现部分警告问题，但 WARNING 级别的事件都会触发一些尝试性的保护逻辑或者恢复逻辑，而且有很大概率能够恢复。

| 事件 ID                 |    数值  |  含义说明                    |
| :-------------------  |:-------- |  :------------------------ |
|TXLIVE_WARNING_NETWORK_BUSY            |  1101| 网络状况不佳：上行带宽太小，上传数据受阻。|
|TXLIVE_WARNING_VIDEO_BLOCK           | 2105 | 当前视频播放出现卡顿 |
