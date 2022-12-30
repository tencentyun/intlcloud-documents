## 学习目标
学习本阶段教程，您将了解并掌握如何对视频加密，并使用播放器播放加密视频。
阅读之前，请先确保已经学习播放器指引的 [阶段1：播放原始视频](https://www.tencentcloud.com/document/product/266/51564) 篇部分，本教程使用了 [阶段1](https://intl.cloud.tencent.com/document/product/266/38098) 篇开通的账号以及上传的视频。

## 步骤1：视频加密
1. 登录云点播控制台，选择 **媒资管理**>[**音视频管理**](https://console.cloud.tencent.com/vod/media)，勾选要处理的视频（FileId 为 387xxxxx8142975036），单击 **音视频处理**：

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7ut4367_1.jpg" width="622" />

2. 在 **媒体处理** 界面：
 - **处理类型** 选择 **任务流**。
 - **任务流模板** 选择 **SimpleAesEncryptPreset**。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GkuI523_2.jpg" width="" style="zoom:100%;" /><span>

>?
>- SimpleAesEncryptPreset 是预置任务流：使用12模板转自适应码流，10模板截图做封面，10模板截雪碧图。
>- 12模板自适应码流是转出加密的多码率输出。

3. 单击**确定**，等待 [任务管理](https://console.cloud.tencent.com/vod/task) 列表中的“任务状态”从“处理中”变为“已完成”，表示视频已处理完毕：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/hUM7408_3.png" style="zoom:80%;" />

4. 进入媒资管理>[**音视频管理**](https://console.cloud.tencent.com/vod/media)，单击发起加密的视频条目右侧 **管理**，进入管理页面：

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ETsG597_4.jpg" width="800" />

选择 **基本信息** 页签：
 - 可以看到生成的封面，以及加密的自适应码流输出（模板 ID 为 12）。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/KBkV486_5.jpg" width="622" />
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/5NsV447_6.jpg" width="700" />

 选择 **截图信息** 页签：
 - 可以看到生成的雪碧图（模板 ID 为 10）。

 <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/XTu8560_7.jpg" width="700" />

## 步骤2：生成播放器签名
本步骤，我们使用签名工具快速生成播放器签名，用于播放器播放视频。
选择 **分发播放设置**>[**播放器签名工具**](https://console.cloud.tencent.com/vod/distribute-play/signature)，填写如下信息：
 - **视频 fileId** 填写 **步骤1** 的  FileId（387xxxxx8142975036）
 - **签名过期时间戳** 播放器签名过期时间，不填表示签名不过期
 - **可播放的视频类型** 选择 **转自适应码流(加密)**
 - **加密类型** 选择 **私有加密（SimpleAES）**
 - **可播放的自适应码流模板** 选择 `Adpative-HLS-Encrypt (12)`
 - **用于缩略图预览的雪碧图** 选择 `SpriteScreenshot (10)`

点击 **生成签名结果**，得到签名结果字符串。

## 步骤3：播放视频
经过步骤2，我们得到播放视频所需的三个参数：`appId`、`fileId` 以及播放器签名（`psign`），下面将展示 Web 端播放视频。

### Web 端播放示例
打开 [Web端播放器体验](https://tcplayer.vcube.tencent.com/)，配置如下：
 - **播放器功能** 选择 **视频播放**
 - 点击 **FileID 播放** 标签页
 - **fileID** 填写上一步的 FileId（387xxxxx8142975036）
 - **appID**  填写文件所属的 appId（即上一步生成播放器签名页面的 appID）
 - **psign** 填写上一步生成的签名结果字符串

点击 **预览** 即可播放视频。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Eapx633_9.png" width="800" />

### 多端播放器 Demo
获取播放器签名后，您可以分别使用 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android) 和 [iOS](https://github.com/LiteAVSDK/Player_iOS)  三端的播放器 Demo 进行验证，具体请参考 Demo 的源码。


## 总结

学习本教程后，您已经掌握如何对视频加密，并在播放器中播放。
