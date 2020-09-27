
### 步骤1：设置频道名称
频道名称用于标识您创建的不同频道。
 ![](https://main.qcloudimg.com/raw/d4bae364e0c3c51d6be78858d85e661d.jpg)

### 步骤2：选择输入
选择要附加到该频道的输入。
如果您的rtp / rtp-fec / udp输入源中有多个音频流，则可以根据封装在mepgts中的音频pid在此处创建选择器，以便您可以在后面的输出配置页面中配置多音频语言。
 ![](https://main.qcloudimg.com/raw/6eb57c71f10a3ad9ec209f218efdc148.jpg)
>!此处的pid必须与输入音频流的pid相同，否则转码任务可能会失败。

### 步骤3：输出组设置
#### 1. 多输出组设置
MediaLive支持一个频道多个output group的输出。点击右上方加号来添加多个output group。
![](https://main.qcloudimg.com/raw/1d1ba42772601106731cc81cc88fca45.jpg)

#### 2. 设置输出组名称和类型
设置当前output group的名称和类型。目前支持MediaLive支持HLS、DASH类型输出，同时支持输出HLS文件至腾讯云COS进行归档（具体操作详见第7节），也支持直接联合Tencent Cloud MediaPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的MediaPackage中（具体操作详见第8节），从而帮助客户形成自己的源站，以便于直播的大规模稳定分发。
![](https://main.qcloudimg.com/raw/e85b466e4310cf22e05a26fdd7cb9f5b.jpg)
>?
>腾讯云对象存储COS介绍详见：[COS产品概述](https://intl.cloud.tencent.com/zh/document/product/436/6222)

#### 3. CDN 推入地址设置
如果您选择了HLS或者DASH协议类型输出，您可在此填写CDN的推入地址。如果您的推送地址具有验证要求，则可以填写验证信息。 
![](https://main.qcloudimg.com/raw/b6e6995cb7c14ce36893fb1c5df99c58.jpg)
#### 4. Segment设置
在您的manifest文件中设置segment长度和segment数量，如果您需要在标签文件中插入utc时间，那么可以打开pdt的开关，并且设置插入utc时间的间隔。
 ![](https://main.qcloudimg.com/raw/9eb8dae8fd4105cef8fa0d3009043d24.jpg)
#### 5. DRM 设置
腾讯云MediaLive支持Tencent DRM及用户自定义DRM，您可基于您的实际需求进行选择。
![](https://main.qcloudimg.com/raw/3d51bc21d6554446339aa2ea857d0dd0.jpg)
>!
- 如果在Output Group Setting中的Output Group Type选择HLS/HLS_ARCHIVE/HLS_MediaPackage，开启DRM则会选择使用Fairplay加密；
- 如果在Output Group Setting中的Output Group Type选择DSAH/DASH_MediaPackage，开启DRM会选择使用Widevine加密。

a. Fairplay密钥配置
当您选择输出类型选择HLS/HLS_ARCHIVE/HLS_MediaPackage时，您此时的加密方式为Fairplay加密，您需要填写Fairplay的ContentId（KeyId）、Key、Iv，其中Key、Iv为32位的16进制字符串。
![](https://main.qcloudimg.com/raw/9d972f049ac9f58f5c3c1e440d0ae38c.jpg)
b. Widevine密钥配置
当您选择输出类型选择DSAH/DASH_MediaPackage时，您此时的加密方式为Widevine加密，Widevine的ContentId及其Track Setting，其中Track类型分SD/HD/UHD1/UHD2/AUDIO。
选择All Track代表指定这五种Track类型的有相同KeyId、Key。
  ![](https://main.qcloudimg.com/raw/ccd46622e810f98f376e0080ceeea93c.jpg)
选择Select Track则可自定义每个Track类型的KeyId和Key。
 ![](https://main.qcloudimg.com/raw/338479820cd026f1c1906ca3c8b82ff9.jpg)

### 6.  音频设置

我们支持一个输出单元来配置多个音频转码，您可在此配置音频模板，包括音频名称，音频转码格式，音频码率以及对应的音频语言，其中如果不关联音频选择器，那么会从input输入流中选择一路默认流进行转码输出。目前支持的音频转码码率范围在6000-1024000bit范围内。语言代码遵循ISO639标准，需要填写3个字符的语言代码。
![](https://main.qcloudimg.com/raw/a3b17971253ef16421b73b5b18e147ad.jpg)
### 7. 视频设置

在此配置视频模板，包括视频模板名；包括编码器类型选择，当前支持H264；包括视频转码码率，支持范围为50000-40000000bit；包括分辨率、帧率配置等等。top speed codec transcoding是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务，Bitrate compression ratio是预期需要降低的视频码率百分比。
![](https://main.qcloudimg.com/raw/960518ebce570f617872941257da7ba7.jpg)
>?
>如果您需要更好的带有智能视频压缩算法的编解码器，您可以选择“极速高清”转码，启用此功能后，AI算法可以根据业务场景实时计算最佳动态编码参数，以实现低比特率和高质量的转码服务。您可以在后面的输入框中填写希望降低的比特率百分比。

### 8. 输出组合
配置Outputs，对已经创建的音频转码模板以及视频转码模板进行组合关联；同时支持在HLS或DASH的文件标签中传递scte35相关的信息。
 ![](https://main.qcloudimg.com/raw/a8076054a9b3c0664f2a876fcf86c0c0.jpg)
## 步骤4：配置完毕

完成上述步骤即配置完毕，点击开始即可运行。