本文针对音视频平台常见的长视频播放场景，推出播放器播放长视频教程。用户将掌握如何在 Web 端、iOS 端、Android 端播放器上播放视频，同时开启 KEY [防盗链](https://www.tencentcloud.com/document/product/266/49274)、自动切换自适应码流、预览视频缩略图、添加视频打点信息。

## 学习目标
学习本阶段教程，您将掌握：
- 如何在云点播设置 KEY 防盗链，实现有效时间、播放人数、播放时长等控制
- 如何在云点播转出自适应码流（播放器能够根据当前带宽，动态选择最合适的码率播放）
- 如何在云点播设置视频打点信息
- 如何在云点播使用雪碧图做缩略图
- 如何使用播放器进行播放

阅读之前，请先确保已经学习播放器指引的 [阶段1：用播放器播放视频](https://intl.cloud.tencent.com/document/product/266/38098) 篇部分，了解云点播 fileid 的概念。

## 操作步骤
### 步骤1：开启 KEY 防盗链
以您账号下的默认分发域名开启 KEY 防盗链为例：
>!请避免直接对生产环境的现网域名开启防盗链，否则可能造成现网的视频无法播放。

1. 登录云点播控制台，选择【分发播放设置】>[【域名管理】](https://console.cloud.tencent.com/vod/distribute-play/domain)，进入设置页面。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pyHf434_1.png" width="800" />

2. 单击“访问控制”页签，找到【Key 防盗链】，点击灰色按钮开启，在弹出的设置页面并单击【随机生成】生成一个随机的 Key，然后单击【确定】保存生效。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/azQ5558_2.jpg" width="522" />

### 步骤2：转出自适应码流与雪碧图
本步骤，我们将指导您如何对视频转出自适应码流与雪碧图。
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod)，选择**视频处理设置**>**模板设置**>**转自适应码流模板**，单击**创建转自适应码流模板**。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3gkP770_3.png)

通过模板创建用户需要的自适应码流，本文创建一条名为 testAdaptive 的自适应码流模板，总共包含三条子流，分辨率分别为480p,720p和1080p。视频码率、视频帧率、音频码率则保持与原视频一致。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/XIga303_4.jpg)

2. 选择**视频处理设置**>**模板设置**>**截图模板**，单击**创建截图模板**。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/mVrf686_5.png)

通过模板创建用户需要的雪碧图，本文创建一个名为 testSprite 的雪碧图模板，采样间隔为5%，小图行数：10，小图列数：10。

![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)

3. 通过任务流，添加自适应码流模板与雪碧图模板。
选择**视频处理设置**>**任务流设置**，单击**创建任务流**。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/sUGF476_7.jpg)

通过任务流，添加用户需要处理的任务，本文为展示播放自适应码流过程，创建了一条 testPlayVideo 的任务流，该任务流仅增加了自适应码流模板和雪碧图模板。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e45517_8.jpg)

4. 选择**媒资管理**>**音视频管理**，勾选需要处理的视频（FileId 为 387xxxxx8142975036），单击**任务流**，选择任务流模板，发起任务。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LAPx726_9.png)

5. 至此，我们可以在**任务中心**>[**音视频管理**](https://console.cloud.tencent.com/vod/task)中，查看任务执行情况，完成后获取任务结果。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrMs396_10.jpg" width="800" />

### 步骤3：增加视频打点信息
本步骤，我们将指导您新增的一组视频打点信息。
1. 进入云点播服务端 API 文档>**媒资管理相关接口**>[**修改媒体文件属性**](https://intl.cloud.tencent.com/document/product/266/37570)，单击调试，进入云 API 控制台进行调试。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3hHA645_11.jpg)
2. 通过参数名称 **AddKeyFrameDescs.N** 添加指定视频打点信息
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dpvW350_12.jpg)
至此您已经完成了在云端上的操作，此时您在云点播已经转出自适应码流，视频雪碧图和添加了相关视频打点信息。

### 步骤4：生成播放器签名
本步骤，我们使用签名工具快速生成播放器签名，用于播放器播放视频。
选择 **分发播放设置**>[**播放器签名工具**](https://console.cloud.tencent.com/vod/distribute-play/signature)，填写如下信息：
 - **视频 fileId** 填写 **步骤2** 使用的  FileId（387xxxxx8142975036）
 - **签名过期时间戳** 播放器签名过期时间，不填表示签名不过期
 - **可播放的视频类型** 选择 **转自适应码流(不加密)**
 - **可播放的自适应码流模板** 选择 `testAdaptive (1429229)`
 - **用于缩略图预览的雪碧图** 选择 `testSprite (131353)`
 - **防盗链&加密配置** 开关打开，配置如下：
  - **链接过期时间** 设置获取的播放链接的防盗链签名过期时间
  - **最多可播放 IP 数** 设置最多允许多少个 IP 不同的终端播放

点击 **生成签名结果**，得到签名结果字符串。


### 步骤5：播放器端集成
经过步骤4，我们得到播放视频所需的三个参数：`appId`、`fileId` 以及播放器签名（`psign`）
本步骤，我们将指导您在 Web 端、iOS 端、Android 端播放器播放自适应码流、添加缩略图与打点信息。

<dx-tabs>
::: Web 端
用户需要集成视立方播放器请参见 [集成指引](https://intl.cloud.tencent.com/document/product/266/33977)，引入播放器 SDK 文件之后，使用 `appId`、`fileId` 以及播放器签名（`psign`）进行播放。

播放器的构建方法为`TCPlayer`, 通过其创建播放器实例即可播放。

#### 1. 在 html 文件放置播放器容器

在需要展示播放器的页面位置加入播放器容器。例如，在 index.html 中加入如下代码（容器 ID 以及宽高都可以自定义）。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### 2. 使用 fileID 播放

在 index.html 页面初始化的代码中加入以下初始化脚本，传入获取到的 fileID 与 appID 即可播放。

```
var player = TCPlayer('player-container-id', { // player-container-id 为播放器容器 ID，必须与 html 中一致
    fileID: '387xxxxx8142975036', // 要播放的视频 fileID
    appID: '1400329073', // 要播放视频的点播账号 appID
    psign:'psignxxxx'   // psign 即播放器签名，签名介绍和生成方式参见链接：https://www.tencentcloud.com/document/product/266/38099
});
```


:::
::: iOS 端
用户需要集成视立方播放器请参见 [集成指引](https://intl.cloud.tencent.com/document/product/266/33976)，集成完后，使用 `appId`、`fileId` 以及播放器签名（`psign`）进行播放。

播放器主类为`SuperPlayerView`，创建后即可播放视频：

```xml
// 引入头文件
#import <SuperPlayer/SuperPlayer.h>

// 创建播放器  
_playerView = [[SuperPlayerView alloc] init];
// 设置代理，用于接受事件
_playerView.delegate = self;
// 设置父 View，_playerView 会被自动添加到 holderView 下面
_playerView.fatherView = self.holderView;
```

#### 使用 fileId 播放

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// 配置 AppId
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"387xxxxx8142975036"; // 配置 FileId
// pSign 即播放器签名，签名介绍和生成方式参见链接：https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = @"psignxxxx";
[_playerView playWithModelNeedLicence:model];
[_playerView playWithModel:model];
```
:::
::: Android 端
集成视立方播放器请参考[集成指引](https://intl.cloud.tencent.com/document/product/266/33975) ，集成完后，使用 `appId`、`fileId` 以及播放器签名（`psign`）进行播放。

播放器主类为`SuperPlayerView`，创建后即可播放视频：

#### 1. 在布局文件创建SuperPlayerView

```xml
<!-- 播放器-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. 使用 fileId 播放

```java
//在布局文件引入SuperPlayerView ，然后创建实例
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);

SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// 配置 AppId
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "387xxxxx8142975036"; // 配置 FileId
// pSign 即播放器签名，签名介绍和生成方式参见链接：https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = "psignxxxx";

mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## 总结

至此，您就可以在播放器播放开启了 KEY 防盗链的点播帐号下的媒体文件，查看雪碧图预览、视频打点信息和自动切换动态自适应码流。
更多播放器功能请参见 [功能说明](https://intl.cloud.tencent.com/document/product/266/42965)。
