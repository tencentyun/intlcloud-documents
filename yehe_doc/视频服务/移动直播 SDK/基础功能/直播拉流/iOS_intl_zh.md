# iOS直播拉流文档
[原文地址](https://github.com/tencentyun/qcloud-documents/blob/master/product/%E8%A7%86%E9%A2%91%E6%9C%8D%E5%8A%A1/%E7%A7%BB%E5%8A%A8%E7%9B%B4%E6%92%AD/%E5%9F%BA%E7%A1%80%E5%8A%9F%E8%83%BD/%E7%9B%B4%E6%92%AD%E6%8B%89%E6%B5%81/iOS.md)

## 基础知识

本文主要介绍视频云 SDK 的直播播放功能。

#### 直播

- **直播（LIVE）**的视频源是主播实时推送的。因此，主播停止推送后，播放端的画面也会随即停止，而且由于是实时直播，所以播放器在播直播 URL 的时候是没有进度条的。

#### 协议的支持

通常使用的直播协议如下，App 端推荐使用 FLV 协议的直播地址（以“http”开头，以“.flv”结尾）：

| 直播协议    | 优点                   | 缺点                 | 播放延迟  |
| ----------- | ---------------------- | -------------------- | --------- |
| FLV         | 成熟度高、高并发无压力 | 需集成 SDK 才能播放  | 2s - 3s   |
| RTMP        | 优质线路下理论延迟最低 | 高并发情况下表现不佳 | 1s - 3s   |
| HLS（m3u8） | 手机浏览器支持度高     | 延迟非常高           | 10s - 30s |

## 特别说明

- **是否有限制？**
  视频云 SDK **不会对**播放地址的来源做限制，即您可以用它来播放腾讯云或非腾讯云的播放地址。但视频云 SDK 中的播放器只支持 FLV 、RTMP两种格式的直播地址。

## 对接攻略

#### step1：创建Player

视频云 SDK 中的 TXLivePlayer 模块负责实现直播播放功能。

```objective-c
TXLivePlayerV2 *txLivePlayer = [[TXLivePlayerV2 alloc] init];
```

#### step2：渲染 View

接下来我们要给播放器的视频画面找个地方来显示，iOS 系统中使用 view 作为基本的界面渲染单位，所以您只需要准备一个 view 并调整好布局就可以了。

```objective-c
[txLivePlayer setRenderView:_myView];
```

内部原理上，播放器并不是直接把画面渲染到您提供的 view （示例代码中的 _myView）上，而是在这个 view 之上创建一个用于 OpenGL 渲染的子视图（subView）。

如果您要调整渲染画面的大小，只需要调整您所常见的 view 的大小和位置即可，SDK 会让视频画面跟着您的 view 的大小和位置进行实时的调整。

![39a02a8525a20fd861c69c42d2b3ab14](https://main.qcloudimg.com/raw/39a02a8525a20fd861c69c42d2b3ab14.png)

**如何做动画？**
针对 view 做动画是比较自由的，不过请注意此处动画所修改的目标属性应该是 transform 属性而不是 frame 属性。

```objective-c
[UIView animateWithDuration:0.5 animations:^{
    _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); //缩小1/3
}];
```

#### step3：启动播放

```objective-c
NSString* flvUrl = @"http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
[txLivePlayer startPlay:flvUrl];
```
#### step4：画面调整

* **view：大小和位置**
  如需修改画面的大小及位置，直接调整 setupVideoWidget 的参数 view 的大小和位置，SDK 会让视频画面跟着您的 view 的大小和位置进行实时的调整。

* **setRenderFillMode：铺满 or 适应**

  | 可选值              | 含义                                                         |
  | ------------------- | ------------------------------------------------------------ |
  | TXLiveFillMode_Fill | 图像铺满屏幕，不留黑边，如果图像宽高比不同于屏幕宽高比，部分画面内容会被裁剪掉。 |
  | TXLiveFillMode_Fit  | 图像适应屏幕，保持画面完整，但如果图像宽高比不同于屏幕宽高比，会有黑边的存在。 |

* **setRenderRotation：画面旋转**

  | 可选值             | 含义            |
  | ------------------ | --------------- |
  | TXLiveRotation_0   | 不旋转          |
  | TXLiveRotation_90  | 顺时针旋转90度  |
  | TXLiveRotation_180 | 顺时针旋转180度 |
  | TXLiveRotation_270 | 顺时针旋转270度 |

  /// TODO 图片周一上传到服务器
  ![截屏2020-08-06 上午10.55.49](/Users/jj/Desktop/截屏2020-08-06 上午10.55.49.png)

#### step5：暂停播放

对于直播播放而言，并没有真正意义上的暂停，所谓的直播暂停，只是**画面冻结**和**关闭声音**，而云端的视频源还在不断地更新着，所以当您调用 resume 的时候，会从最新的时间点开始播放，这是和点播对比的最大不同点（点播播放器的暂停和继续与播放本地视频文件时的表现相同）。

```objective-c
// 暂停声音
[txLivePlayer pauseAudio];
// 恢复声音
[txLivePlayer resumeAudio];

// 暂停视频
[txLivePlayer pauseVideo];
// 恢复视频
[txLivePlayer resumeVideo];
```

#### step6：结束播放

结束播放，调用**stopPlay**。

```objective-c
// 停止播放
[txLivePlayer stopPlay];
```

#### step7：消息接收

此功能可以在推流端将一些自定义 message 随着音视频线路直接下发到观众端，适用场景例如：

- 冲顶大会：推流端将**题目**下发到观众端，可以做到“音-画-题”完美同步。
- 秀场直播：推流端将**歌词**下发到观众端，可以在播放端实时绘制出歌词特效，因而不受视频编码的降质影响。
- 在线教育：推流端将**激光笔**和**涂鸦**操作下发到观众端，可以在播放端实时地划圈、划线。

通过如下方案可以使用此功能：

* TXLivePlayer 通过 **TXLivePlayerObserver** 监听消息

```objective-c
- (void)onRecvSEIMessage:(id<TXLivePlayerV2>)player message:(NSData *)msg {
    NSString *receiveMsg = [[NSString alloc] initWithData:msg encoding:NSUTF8StringEncoding];
    [self makeToastTip:receiveMsg];
}
```

#### step8：屏幕截图

通过调用 **snapshot** 您可以截取当前直播画面为一帧屏幕，此功能只会截取当前直播流的视频画面，如果您需要截取当前的整个 UI 界面，请调用 iOS 的系统 API 来实现。

```objective-c
// 腾讯云音视频通话功能的回调通知
- (TXLiveCode)snapshot:(id<TXLiveSnapshotObserver>)observer;

// 截屏回调
@protocol TXLiveSnapshotObserver <NSObject>
@optional
- (void)onSnapshotComplete:(TXImage *)image;
@end
```

## 延时调整

腾讯云 SDK 的直播播放（LVB）功能，并非基于 ffmpeg 做二次开发， 而是采用了自研的播放引擎，所以相比于开源播放器，在直播的延迟控制方面有更好的表现，我们提供了三种延迟调节模式，分别适用于：秀场，游戏以及混合场景。

* **三种模式的特性对比**

  | 控制模式 | 卡顿率     | 平均延迟 | 适用场景             | 原理简述                                                   |
  | :------- | :--------- | :------- | :------------------- | :--------------------------------------------------------- |
  | 极速模式 | 较流畅偏高 | 2s- 3s   | 美女秀场（冲顶大会） | 在延迟控制上有优势，适用于对延迟大小比较敏感的场景         |
  | 流畅模式 | 卡顿率最低 | >= 5s    | 游戏直播（企鹅电竞） | 对于超大码率的游戏直播（例如绝地求生）非常适合，卡顿率最低 |
  | 自动模式 | 网络自适应 | 2s-8s    | 混合场景             | 观众端的网络越好，延迟就越低；观众端网络越差，延迟就越高   |

* **三种模式的对接代码**

  ```objective-c
  #define CACHE_TIME_FAST             1.0f
  #define CACHE_TIME_SMOOTH           5.0f
  
  //极速模式
  [_player setCacheParams:CACHE_TIME_FAST maxTime:CACHE_TIME_FAST];
  
  //流畅模式
  [_player setCacheParams:CACHE_TIME_SMOOTH maxTime:CACHE_TIME_SMOOTH];
  
  //自动模式
  [_player setCacheParams:CACHE_TIME_FAST maxTime:CACHE_TIME_SMOOTH];
  ```


## SDK事件监听

您可以为 TXLivePlayer 对象绑定一个 **TXLivePlayerObserver**，之后 SDK 的内部状态信息均会通过 **onConnectionStateUpdate**和**onStatisticsUpdate**通知给您。

#### 连接状态更新回调

```objective-c
- (void)onConnectionStateUpdate:(id<TXLivePlayerV2>)player
                          state:(TXLivePlayerConnectionState)state
                        message:(NSString *)msg
                      extraInfo:(NSDictionary *)extraInfo;
```

#### 播放开始事件

| 事件ID                                             | 数值 | 含义说明       |
| -------------------------------------------------- | ---- | -------------- |
| TXLivePlayerConnectionState_StartConnectServer     | 0    | 正在连接服务器 |
| TXLivePlayerConnectionState_ConnectServerSuccess   | 1    | 连接服务器成功 |
| TXLivePlayerConnectionState_StartReconnectServer   | 2    | 开始重连服务器 |
| TXLivePlayerConnectionState_StartLoading           | 3    | 开始缓冲       |
| TXLivePlayerConnectionState_ReconnectServerSuccess | 5    | 重连服务器成功 |

#### 播放结束事件

| 事件ID                                       | 数值 | 含义说明         |
| -------------------------------------------- | ---- | ---------------- |
| TXLivePlayerConnectionState_LoadFinish       | 4    | 缓冲结束         |
| TXLivePlayerConnectionState_DisconnectServer | 6    | 与服务器断开连接 |

#### 警告事件回调

```objective-c
- (void)onWarning:(id<TXLivePlayerV2>)player
             code:(TXLiveCode)code
          message:(NSString *)msg
        extraInfo:(NSDictionary *)extraInfo;
```

#### 警告码

* 通用警告码（不归属网络、音频、视频）

  区段：7000000 ~ 7000999

  | 警告码ID  | 数值 | 含义说明 |
  | --------- | ---- | -------- |
  | TXLIVE_OK | 0    | 成功播放 |

* 网络模块警告码

  区段：7001000 ~ 7001999

  | 警告码ID                    | 数值    | 含义说明 |
  | --------------------------- | ------- | -------- |
  | TXLIVE_WARNING_NETWORK_BUSY | 7001000 | 网络繁忙 |

* 视频模块警告码

  区段：7002000 ~ 7002999

  | 警告码ID                   | 数值    | 含义说明     |
  | -------------------------- | ------- | ------------ |
  | TXLIVE_WARNING_VIDEO_BLOCK | 7002000 | 视频获取失败 |

#### 错误事件回调

```objective-c
- (void)onError:(id<TXLivePlayerV2>)player
           code:(TXLiveCode)code
        message:(NSString *)msg
      extraInfo:(NSDictionary *)extraInfo;
```

#### 错误码

* 通用错误码

  区段：-7001000 ~ -7001999

  | 错误码ID                       | 数值     | 含义说明 |
  | ------------------------------ | -------- | -------- |
  | TXLIVE_ERROR_NOT_SUPPORTED     | -7001000 | 不被支持 |
  | TXLIVE_ERROR_INVALID_PARAMETER | -7001001 | 参数非法 |
  | TXLIVE_ERROR_REFUSED           | -7001002 | 被拒绝   |
  | TXLIVE_ERROR_NOT_READY         | -7001003 | 还未准备 |

* 摄像头相关错误码

  区段：-7002000 ~ -7002999

  | 错误码ID                          | 数值     | 含义说明           |
  | --------------------------------- | -------- | ------------------ |
  | TXLIVE_ERROR_CAMERA_START_FAILED  | -7002000 | 摄像头开启失败     |
  | TXLIVE_ERROR_CAMERA_OCCUPIED      | -7002001 | 摄像头被占用       |
  | TXLIVE_ERROR_CAMERA_NO_PERMISSION | -7002002 | 摄像头没有访问权限 |

* 麦克风相关错误码

  区段：-7003000 ~ -7003999

  | 错误码ID                              | 数值     | 含义说明           |
  | ------------------------------------- | -------- | ------------------ |
  | TXLIVE_ERROR_MICROPHONE_START_FAILED  | -7003000 | 麦克风开启失败     |
  | TXLIVE_ERROR_MICROPHONE_OCCUPIED      | -7003001 | 麦克风被占用       |
  | TXLIVE_ERROR_MICROPHONE_NO_PERMISSION | -7003002 | 麦克风没有访问权限 |

* 屏幕录制相关错误码

  区段：-7004000 ~ -7004999

  | 错误码ID                                  | 数值     | 含义说明       |
  | ----------------------------------------- | -------- | -------------- |
  | TXLIVE_ERROR_SCREEN_CAPTURE_NOT_SUPPORTED | -7004000 | 不支持屏幕录制 |
  | TXLIVE_ERROR_SCREEN_CAPTURE_START_FAILED  | -7004001 | 屏幕录制失败   |
  | TXLIVE_ERROR_SCREEN_CAPTURE_INTERRUPTED   | -7004002 | 屏幕录制中断   |

* RTMP专属错误码

  区段：-3000 ~ -3999

  | 错误码ID                          | 数值     | 含义说明 |
  | --------------------------------- | -------- | -------- |
  | TXLIVE_ERROR_INVALID_RTMP_LICENSE | -7005001 | RTMP非法 |

## 获取视频分辨率

通过 onVideoResolutionChanged 回调，可以获取视频流当前的宽高比，这是获取视频流分辨率的最快速办法，大约会在启动播放后的100ms - 200ms左右就能得到。

```objective-c
- (void)onVideoResolutionChanged:(id<TXLivePlayerV2>)player
                           width:(NSInteger)width
                          height:(NSInteger)height;
```

| 参数   | 含义     | 数值               |
| :----- | :------- | :----------------- |
| width  | 视频宽度 | 分辨率数值，如1920 |
| height | 视频高度 | 分辨率数值，如1080 |

## 定时触发的状态通知

**onStatisticsUpdate** 通知每秒都会被触发一次，目的是实时反馈当前的推流器状态，它就像汽车的仪表盘，可以告知您目前 SDK 内部的一些具体情况，以便您能对当前网络状况和视频信息等有所了解。

```objective-c
- (void)onStatisticsUpdate:(id<TXLivePlayerV2>)player
                statistics:(TXLivePlayerStatistics *)statistics;
```

| 评估参数     | 含义说明                     |
| ------------ | ---------------------------- |
| appCpu       | 当前 App 的 CPU 使用率（％） |
| systemCpu    | 当前系统的 CPU 使用率（％）  |
| width        | 视频宽度                     |
| height       | 视频高度                     |
| fps          | 帧率（fps）                  |
| videoBitrate | 视频码率（Kbps）             |
| audioBitrate | 音频码率（Kbps）             |

