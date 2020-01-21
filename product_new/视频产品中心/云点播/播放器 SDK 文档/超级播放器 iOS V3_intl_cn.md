## 简介

iOS 超级播放器 SDK 是一款用于播放云点播视频的播放器组件，几行代码就能实现类似腾讯视频强大的播放功能。

* 基础功能：横竖屏切换、清晰度选择、手势和小窗等。
* 高级功能：视频缓存、软硬解切换、倍速播放、视频缩略图、DRM 加密播放等。

相比系统播放器，超级播放器支持格式更多，兼容性更好，功能更强大。同时还具备首屏秒开和低延迟的优点。

## SDK 下载

云点播 iOS 超级播放器的下载地址是 [SuperPlayer_iOS](https://github.com/tencentyun/SuperPlayer_iOS)。

## 快速集成

### CocoaPods 集成

请将下面代码加入到您的 Podfile 中：
```
pod 'SuperPlayer'
```

命令行输入`pod install`或`pod update`执行安装。

### 准备视频

登录 [云点播控制台](https://console.cloud.tencent.com/vod/overview)，单击左侧菜单栏的【媒资管理】，在“**已上传**”栏的视频列表中，将看到上传完成的视频，以及视频对应的 ID（即 FileId）。如果您还没有视频，请先单击【上传视频】，上传一个视频。
![](https://main.qcloudimg.com/raw/5aa5675fb0b702b447e422328f54cb72.png)

通过 [ProcessMedia](#APIhttps://intL.cloud.tencent.com/document/product/266/33427) ，对上传的视频发起 [转自适应码流](https://intl.cloud.tencent.com/document/product/266/33942) 任务：
API 参数中的`MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition`建议填10，表示转 HLS 格式的自适应码流。

### 开始播放

播放器主类为`SuperPlayerView`，创建后即可播放视频。
```objective-c
// 引入头文件
#import <SuperPlayer/SuperPlayer.h>
_playerView = [[SuperPlayerView alloc] init];
// 设置代理，用于接受事件
_playerView.delegate = self;
// 设置父View，_playerView会被自动添加到holderView下面
_playerView.fatherView = self.holderView;
SuperPlayerModel *playerModel = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *video = [[SuperPlayerVideoId alloc] init];
//设置播放信息
video.appId = 1256993030;  //AppId
video.fileId = @"7447398157015849771";  //视频 FileId
video.playDefinition = @"10";   //播放模板 ID
video.version = FileIdV3;
playerModel.videoId = video;
// 开始播放
[_playerView playWithModel:self.playerModel];
```

代码中的`appId`是您的 AppId，`fileId`是您要播放的视频 ID，`playDefinition`是您播放时使用的播放模板ID，`version`固定填`SuperPlayerVideoId.FILE_ID_V3`。

运行代码，可以看到视频在手机上播放，并且界面上大部分功能都处于可用状态。
<img src="https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png" width="550">

## 缩略图与打点

在播放视频时，进度条上的“缩略图”和“打点信息”，有助于观众找到感兴趣的点。缩略图通过 [雪碧图](#APIhttps://intl.cloud.tencent.com/document/product/266/8101) 实现，视频打点需要 [修改媒资中的打点信息](#APIhttps://intl.cloud.tencent.com/document/product/266/31762#.E7.A4.BA.E4.BE.8B3-.E4.BF.AE.E6.94.B9.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6.E8.A7.86.E9.A2.91.E6.89.93.E7.82.B9.E4.BF.A1.E6.81.AF)。

为视频截取雪碧图，并添加打点信息后，播放器的界面会增加新的元素。
<img src="https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png" width="550">

## 小窗播放

小窗播放是指在 App 内，悬浮在主窗口上的播放器。使用小窗播放非常简单，只需要在适当位置调用下面代码即可：

```objective-c
[SuperPlayerWindow sharedInstance].superPlayer = _playerView; // 设置小窗显示的播放器
[SuperPlayerWindow sharedInstance].backController = self;  // 设置返回的view controller
[[SuperPlayerWindow sharedInstance] show]; // 悬浮显示
```
<img src="https://main.qcloudimg.com/raw/e2ee64230af1b9c3a79cad935afa8b6a.jpeg" width="300">

## 退出播放

如果不需要播放器，可以调用`resetPlayer`清理播放器内部状态，释放内存。
```objective-c
[_playerView resetPlayer];
```

## 更多功能

完整功能可扫码下载视频云工具包体验，或直接运行工程 Demo。
<img src="https://main.qcloudimg.com/raw/b670e99ddb3f0d828798520e19f40fa7.png" width="150">
