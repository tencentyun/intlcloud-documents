## 学习目标
通过本阶段的教程后，您将掌握上传一个视频到云点播，并在播放器中播放的技能。

## 前置条件
在开始本教程之前，请您确保已满足以下前置条件。

### 开通云点播
您需要开通云点播，步骤如下：

1. 注册 [腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
2. 购买云点播服务，具体请参见 [计费概述](https://intl.cloud.tencent.com/document/product/266/2838)。
3. 选择 **云产品**>**视频服务**>[**云点播**](https://console.cloud.tencent.com/vod)，进入云点播控制台。

至此，您已经完成了云点播的开通步骤。

## 步骤1：上传视频
本步骤，我们将指导您如何上传视频。

1. 登录云点播控制台，选择 **媒资管理**>[ **音视频管理** ](https://console.cloud.tencent.com/vod/media)，单击 **上传音视频**。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/eDZY097_1.jpg" width="722" />

2. 在上传界面，选择 **本地上传**，并单击 **选择文件** 上传本地视频，其他设置如下：
	- **视频处理** 选择 **只上传，暂不进行视频处理**。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zB6K038_2.jpg)

3. 单击 **开始上传**，进入“正在上传”页，当 **状态** 变为 **上传成功** 即表示上传完成，**文件 ID** 即为上传音视频的 FileId（这里为 387xxxxx8142975036）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nMEx197_3.jpg)

## 步骤2：生成播放器签名
本步骤，我们使用签名工具快速生成播放器签名，用于播放器播放视频。
选择 **分发播放设置**>[**播放器签名工具**](https://console.cloud.tencent.com/vod/distribute-play/signature)，填写如下信息：
 - **视频 fileId** 填写 **步骤1** 的  FileId（387xxxxx8142975036）
 - **签名过期时间戳** 播放器签名过期时间，不填表示签名不过期
 - **可播放的视频类型** 选择 **原始视频**

点击 **生成签名结果**，得到签名结果字符串。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3pgW155_4.jpg" width="800" />

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
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/SfPg988_5.png" width="800" />

### 多端播放器 Demo
获取播放器签名后，您可以分别使用 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/LiteAVSDK/Player_Android) 和 [iOS](https://github.com/LiteAVSDK/Player_iOS)  三端的播放器 Demo 进行验证，具体请参考 Demo 的源码。


## 总结

学习本教程后，您已经掌握如何上传一个视频到云点播，并在播放器中播放。

如果您希望：
- 播放转码视频，请参考 [阶段2：播放转码视频](https://www.tencentcloud.com/document/product/266/51565)
- 播放自适应码流视频，请参考 [阶段3：播放自适应码流视频](https://www.tencentcloud.com/document/product/266/51566)
- 播放加密视频，请参考 [阶段4：播放加密视频](https://www.tencentcloud.com/document/product/266/51556)
- 播放长视频方案，请参考 [阶段5：播放长视频方案](https://www.tencentcloud.com/document/product/266/51557)