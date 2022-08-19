StreamLive 支持不同类型的输出，您可以在此步骤中创建输出及输出组。

## 设置多输出组
StreamLive支持对一个频道设置多个Output Group输出，可以通过点击右上方的**加号**来添加多个Output Group。
![](https://qcloudimg.tencent-cloud.cn/raw/3e13eac666167d0f867e51e8a97cc1f0.png)

## 设置输出组名称和类型
对Output Group设置名称和类型：
![](https://qcloudimg.tencent-cloud.cn/raw/6b239c37c95f0cc226bc93e12a481395.png)
目前支持HLS、DASH、HLS_STREAM_PACKAGE、DASH_STREAM_PACKAGE、HLS_ARCHIVE、DASH_ARCHIVE类型输出：

- HLS、DASH通过HTTP PUT协议，输出到Destination。
- HLS_STREAM_PACKAGE、DASH_STREAM_PACKAGE通过HTTP PUT协议，输出至同账号下的[StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45219)中。从而帮助客户形成自己的源站，用于给直播CDN进行直播回源。
- HLS_ARCHIVE、DASH_ARCHIVE支持将直播内容输出到[腾讯云COS](https://intl.cloud.tencent.com/document/product/1048/45218)进行归档。

## 设置目标地址
- 如果您选择了HLS或DASH协议类型输出，您可在此填写CDN的推流地址。如果您的推流地址具有验证要求，则可以填写验证信息。
![](https://qcloudimg.tencent-cloud.cn/raw/e76f39828aade1c04c31b17e521220ed.png)
- 如果您选择了HLS_STREAM_PACKAGE或DASH_STREAM_PACKAGE协议类型输出，您可在此填写**StreamPackage Channel Id**，StreamLive会将直播内容推送到StreamPackage中。
![](https://qcloudimg.tencent-cloud.cn/raw/05cae1db0fcfe74a723a0d828e3f5485.png)
- 如果您选择了HLS_ARCHIVE或DASH_ARCHIVE协议类型输出，您可以在此填写**COS Destination**，StreamLive会将近7天的直播内容归档至COS中。（每次重新启动后会覆盖）
![](https://qcloudimg.tencent-cloud.cn/raw/15f727c5101320835259eeb4b0f82529.png)

## 设置DRM
腾讯云StreamLive支持开启DRM加密，其中支持用户自定义秘钥（CustomDRMKeys）和SDMCDRM，您可基于您的实际需求进行选择，具体使用方式您可以参考[DRM配置文档](https://intl.cloud.tencent.com/document/product/1048/45217)。
![](https://qcloudimg.tencent-cloud.cn/raw/8d81955db11e160cb0be5e2a8ed9226a.png)

## 设置转码模板
转码模板支持合并式的音视频转码以及分离式音视频转码，您可以根据实际需求进行选择。其主要区别是针对HLS类的输出，分离式音视频转码可支持多音轨（多音频）自由组合搭配，如无此需求，建议使用合并式的音视频转码模板。
- 合并式的音视频转码模板：一次性配置音频和视频转码配置。
![](https://qcloudimg.tencent-cloud.cn/raw/5567d7eff345ae787a98f4e5c0692bc9.png)
- 分离式的音视频转码模板：需要单独分别配置音频转码模板和视频转码模板。
![](https://qcloudimg.tencent-cloud.cn/raw/aa81355608bc2ad72eab06e043a88fb3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/00196f0a0566111d33a4aef484809110.png)
>!  **Top Speed Codec Transcoding**是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数，以实现低码率、高质量的转码服务。**Bitrate Compression Ratio**是预期需要降低的视频码率百分比。

### 设置输出
- 使用合并式转码模板输出，每个Output只能选择一个转码模板，作为多码率输出中的其中一个转码档位。
![](https://qcloudimg.tencent-cloud.cn/raw/b007445cb3f47a9ec6d827f959cff9ba.png)
- 使用分离式转码模板输出，每个Output可以选取一个视频转码模板和多个音频转码模板。其中视频转码模板作为多码率输出中的其中一个转码档位，音频转码模板则表示该转码档位可以搭配的音轨（音频）。
![](https://qcloudimg.tencent-cloud.cn/raw/8b758ded635531a9a24f1aae51eb9828.png)

### 完成配置
点击**Done**保存配置。至此，整个频道已经配置完毕。点击【Start】即可运行。
![](https://qcloudimg.tencent-cloud.cn/raw/a596817ccf73cd4573f83e3d572fcbee.png)