
## 步骤1：设置频道名称
频道名称用于标识您创建的不同频道。
 ![](https://main.qcloudimg.com/raw/d4bae364e0c3c51d6be78858d85e661d.jpg)

## 步骤2：选择输入
选择要附加到该频道的输入。
如果您的 rtp / rtp-fec / udp 输入源中有多个音频流，则可以根据封装在 mepgts 中的音频 pid 在此处创建选择器，以便您可以在后面的输出配置页面中配置多音频语言。
 ![](https://main.qcloudimg.com/raw/6eb57c71f10a3ad9ec209f218efdc148.jpg)

> !此处的 pid 必须与输入音频流的 pid 相同，否则转码任务可能会失败。

## 步骤3：输出组设置
### 1. 多输出组设置
MediaLive 支持一个频道多个 output group 的输出。点击右上方加号来添加多个 output group。
![](https://main.qcloudimg.com/raw/1d1ba42772601106731cc81cc88fca45.jpg)

### 2. 设置输出组名称和类型
设置当前 output group 的名称和类型。目前 MediaLive 支持HLS、DASH类型输出，同时支持输出 HLS 文件至腾讯云 COS 进行归档，相关操作可参见 [输出HLS文件至腾讯云COS归档](https://intl.cloud.tencent.com/document/product/1048/38361)，也支持直接联合 Tencent Cloud MediaPackage 一起使用，将 HLS/DASH 格式直播流直接输出至同账号下的 MediaPackage 中，相关操作可参见【将直播流输出至MediaPackage】，从而帮助客户形成自己的源站，以便于直播的大规模稳定分发。
![](https://main.qcloudimg.com/raw/e85b466e4310cf22e05a26fdd7cb9f5b.jpg)

> ?腾讯云对象存储 COS 介绍详见：[COS产品概述](https://intl.cloud.tencent.com/zh/document/product/436/6222)

### 3. CDN 推入地址设置
如果您选择了 HLS 或者 DASH 协议类型输出，您可在此填写 CDN 的推入地址。如果您的推送地址具有验证要求，则可以填写验证信息。 
![](https://main.qcloudimg.com/raw/b6e6995cb7c14ce36893fb1c5df99c58.jpg)

### 4. Segment 设置
在您的 manifest 文件中设置 segment 长度和 segment 数量，如果您需要在标签文件中插入 utc 时间，那么可以打开 pdt 的开关，并且设置插入 utc 时间的间隔。
 ![](https://main.qcloudimg.com/raw/9eb8dae8fd4105cef8fa0d3009043d24.jpg)

### 5. DRM 设置
腾讯云 MediaLive 支持 Tencent DRM 及用户自定义 DRM，您可基于您的实际需求进行选择。
![](https://main.qcloudimg.com/raw/3d51bc21d6554446339aa2ea857d0dd0.jpg)

>!
>- 如果在 Output Group Setting 中的 Output Group Type 选择 HLS/HLS_ARCHIVE/HLS_MediaPackage， 开启DRM则会选择使用 Fairplay 加密。
>- 如果在 Output Group Setting中的 Output Group Type 选择 DSAH/DASH_MediaPackage，开启 DRM 会选择使用 Widevine 加密。

a. Fairplay 密钥配置
当您选择输出类型选择 HLS/HLS_ARCHIVE/HLS_MediaPackage 时，您此时的加密方式为 Fairplay 加密，您需要填写 Fairplay 的 ContentId（KeyId）、Key、Iv，其中 Key、Iv 为32位的16进制字符串。
![](https://main.qcloudimg.com/raw/9d972f049ac9f58f5c3c1e440d0ae38c.jpg)
b. Widevine 密钥配置
当您选择输出类型选择 DSAH/DASH_MediaPackage 时，您此时的加密方式为 Widevine 加密，Widevine 的ContentId 及其 Track Setting，其中 Track 类型分 SD/HD/UHD1/UHD2/AUDIO。
选择 All Track 代表指定这五种Track类型的有相同 KeyId、Key。
  ![](https://main.qcloudimg.com/raw/ccd46622e810f98f376e0080ceeea93c.jpg)
选择 Select Track 则可自定义每个 Track 类型的 KeyId 和 Key。
 ![](https://main.qcloudimg.com/raw/338479820cd026f1c1906ca3c8b82ff9.jpg)

### 6.  音频设置

我们支持一个输出单元来配置多个音频转码，您可在此配置音频模板，包括音频名称，音频转码格式，音频码率以及对应的音频语言，其中如果不关联音频选择器，那么会从 input 输入流中选择一路默认流进行转码输出。目前支持的音频转码码率范围在 6000-1024000bit 范围内。语言代码遵循 ISO639 标准，需要填写3个字符的语言代码。
![](https://main.qcloudimg.com/raw/a3b17971253ef16421b73b5b18e147ad.jpg)

### 7. 视频设置

在此配置视频模板，包括视频模板名；包括编码器类型选择，当前支持H264；包括视频转码码率，支持范围为 50000-40000000bit；包括分辨率、帧率配置等等。top speed codec transcoding 是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过 AI 算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务，Bitrate compression ratio 是预期需要降低的视频码率百分比。
![](https://main.qcloudimg.com/raw/960518ebce570f617872941257da7ba7.jpg)

>?
>如果您需要更好的带有智能视频压缩算法的编解码器，您可以选择“极速高清”转码，启用此功能后，AI算法可以根据业务场景实时计算最佳动态编码参数，以实现低比特率和高质量的转码服务。您可以在后面的输入框中填写希望降低的比特率百分比。

### 8. 输出组合
配置 Outputs，对已经创建的音频转码模板以及视频转码模板进行组合关联；同时支持在 HLS 或 DASH 的文件标签中传递 scte35 相关的信息。
 ![](https://main.qcloudimg.com/raw/a8076054a9b3c0664f2a876fcf86c0c0.jpg)

## 步骤4：配置完毕

上述步骤即配置完毕之后，点击开始即可运行。
