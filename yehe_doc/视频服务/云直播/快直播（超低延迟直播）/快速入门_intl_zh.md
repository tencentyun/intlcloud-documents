本教程将指引您快速了解快直播服务。在您使用快直播服务前，建议您提前阅读快直播 [价格总览](https://intl.cloud.tencent.com/document/product/267/2819)，了解**收费项目**和**价格**，避免产生误解。

[](id:step0)
## 准备工作
1. 注册 [腾讯云账号](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)，未进行实名认证的用户无法购买中国境内的云直播实例。
2. 进入 [腾讯云直播服务开通页](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)，勾选同意《腾讯云服务协议》，并单击 **申请开通** 即可开通云直播服务。
>?  
>- 云直播服务申请开通后，会赠送20GB国内播放流量免费体验使用。
>- 域名配置与标准直播一致，如您已接入标准直播，可直接从 [步骤4：获取播放地址](#step4) 部分了解快直播拉流。

[](id:step1)

## 步骤1：添加域名
使用云直播服务，至少需要**2**个域名，一个作为**推流域名**，一个作为**播放域名**，推流和播放不能使用相同的域名。
您可通过使用[ **自有域名** ](https://intl.cloud.tencent.com/document/product/267/35970)添加已完成备案的自有域名。

1. 准备自有域名，如果要在中国内地（大陆）使用需要完成域名备案。

2. 登录云直播控制台，进入[ **域名管理** ](https://console.cloud.tencent.com/live/domainmanage)。

3. 进入自有域名添加页， 单击 **添加域名** 。

   ![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- 云直播默认提供测试域名 `xxxx.livepush.myqcloud.com`，您可通过该域名进行推流测试，但不建议您在正式业务中使用这个域名作为推流域名。
>- 域名添加成功后，您可通过 **域名管理** 的域名列表查看域名信息。若您需要对已添加成功的域名进行管理，请参见 [域名管理](https://intl.cloud.tencent.com/document/product/267/31056)。
>- 更多直播域名相关信息，请参见 [直播基础相关问题](https://intl.cloud.tencent.com/document/product/267/7968)。
5. 域名添加成功后，系统会为您自动分配一个 CNAME 域名（以 `.tlivecdn.com` 或 `.tlivepush.com` 为后缀）。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后即可享受云直播服务。以DNS 服务商为腾讯云为例，添加 CNAME 记录操作步骤如下：[](id:step1_1_1)
    1. 登录 [域名服务控制台](https://console.cloud.tencent.com/domain)。
    2. 选择您需添加 CNAME 的域名，单击 **解析**。
    3. 进入域名的解析页面，单击 **添加记录**。
    4. 在该新增列填写域名前缀为主机记录，选择记录类型为 CNAME，填写 CNAME 域名为记录值。
    5. 单击 **保存** 即可添加 CNAME 记录。
>!
>- CNAME 成功后通常需要一定时间生效，CNAME 不成功是无法使用云直播的。
>- 域名 CNAME 成功后，在云直播控制台的[ **域名管理** ](https://console.cloud.tencent.com/live/domainmanage)列表中可见域名 CNAME 地址状态符号变成 ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)。
>- 若 CNAME 操作后，检测始终不成功，建议您向您的域名注册服务商咨询。
>- 如果您使用其他 DNS 服务商，更多操作请参见 [配置域名 CNAME](https://intl.cloud.tencent.com/document/product/267/31057)。

## 步骤2：获取推流地址

1. 选择 **直播工具箱**>[**地址生成器** ](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)。
2. 进入地址生成器页面，并进行如下配置：
   1. 选择生成类型：**推流域名**。
   2. 选择您在域名管理中已添加的推流域名。
   3. 填写自定义的流名称 StreamName，例如：`liveteststream`。
   4. 选择地址过期时间，例如：`2021-05-25  23:59:59`。
   5. 单击  **生成地址** 即可生成推流地址。
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- 推流地址的结构如下，`live` 为默认的 AppName，`txSecret` 为播放推流的签名，`txTime` 为推流地址的有效时间。
>- 除上述方法，您还可以在云直播控制台的[ **域名管理** ](https://console.cloud.tencent.com/live/domainmanage)中，选择推流域名单击 **管理** ，选择 **推流配置** ，输入推流地址的过期时间和自定义的流名称 StreamName，单击 **生成推流地址** 即可生成推流地址。
>- 您可根据实际业务需求，在生成推流地址前配置创建对应的 [功能模板](https://intl.cloud.tencent.com/document/product/267/31069)，并关联到推流域名下。增值功能价格请参见 [价格总览](https://intl.cloud.tencent.com/document/product/267/2819)。

[](id:step3)
## 步骤3：直播推流

您可根据业务场景将生成好的推流地址输入到对应的推流软件中。
- PC 端推流，建议使用 OBS 推流，具体操作请参见 [OBS 推流](https://intl.cloud.tencent.com/document/product/267/31569)。
- Web 端推流，建议使用 **辅助工具**>[**Web 推流**](https://console.cloud.tencent.com/live/tools/webpush)，选择您需推流的域名，填写自定义的流名称 StreamName，选择地址过期时间，打开摄像头，单击 **开始推流** 即可。    
- 移动端推流，下载安装 [TCToolkit App](https://intl.cloud.tencent.com/document/product/1071/38147)，打开选择 **移动直播 MLVB**>**推流演示（摄像头推流）**，手动输入或扫描二维码录入推流地址到地址编辑框内，单击 **开始推流** 即可。

>? 
>- 定制化的 App 可以集成腾讯云提供的 [移动直播 SDK](https://intl.cloud.tencent.com/document/product/1071) 来实现您的推流功能。
>- 快直播 Web 方案不支持 B 帧解码播放，具体请参见 [关于 B 帧](#b_frame)。

[](id:step4)
## 步骤4：获取播放地址

1. 推流成功后，选择[ **流管理** ](https://console.cloud.tencent.com/live/streammanage)> **在线流**，查看推流地址状态，单击 **测试** 在线播放观看。
2. 选择 **直播工具箱**>[**地址生成器** ](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) 获取播放地址，在该页面进行如下配置：
   1. 选择生成类型，例如：播放域名。
   2. 选择您在域名管理中已添加的播放域名。
   3. 填写与推流地址相同的 StreamName，播放地址` StreamName` 要与推流地址 `StreamName` 一致才能播放对应的流。
   4. 选择地址过期时间，例如：`2021-05-25  23:59:59`。
   5. 根据实际需求选择绑定转码模板。（若选择转码模板，生成的播放地址为转码后的直播播放地址。若需播放原始直播流，则无需选择转码模板生成地址。）
   5. 单击  **生成地址** 即可生成播放地址，快直播拉流 URL 格式为 `webrtc://domain/path/stream_id`。
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
3. 您可以根据业务场景使用以下方式测试直播流是否能正常播放：
   - **Web 端直播流测试**：建议您使用 [WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) 工具进行播放体验。
>?
>- WebRTC Live Demo 支持多清晰度功能，可在云直播控制台 **功能配置**>[**直播转码** ](https://console.cloud.tencent.com/live/config/transcode)配置高清-HD、标清-SD 的转码模板，将带有转码模板的 WebRTC 流地址填入 Demo 中对应的栏目后测试播放（如不需要测试此功能则只需要在 Demo 中填入一条 WebRTC 原始流即可）。
>- 直播转码操作指引及转码计费内容，请参见文档 [直播转码](https://intl.cloud.tencent.com/document/product/267/31071)。
   - **移动端直播流测试**：建议您下载安装 [TCToolkit App](https://intl.cloud.tencent.com/document/product/1071/38147) 打开选择 **快直播播放**，手动输入或扫描 **推流体验** 中得到的快直播播放地址，单击播放按钮播放观看。
>? 如需在 App 中进行推流，可以集成 [移动直播 SDK](https://intl.cloud.tencent.com/product/mlvb) 配合快直播服务使用。使用过程中如果您遇到问题，请参见 [常见问题](#que)。

## 步骤5：快直播产品接入
**移动端方案**：支持 B 帧解码、AAC 音频格式，目前已集成至移动直播 SDK，接入方法请参见 [快直播拉流](https://intl.cloud.tencent.com/document/product/1071/41875)。

[](id:que)
## 常见问题
[](id:play_url)
### 拉流 URL 生成
快直播的拉流 URL 与腾讯云直播拉流 URL 基本一样，只需要将腾讯云直播拉流 URL 前面的 `rtmp` 替换为 `webrtc`。

快直播拉流 URL 格式为 **`webrtc://domain/path/stream_id`**，如果需要 [防盗链鉴权](https://intl.cloud.tencent.com/document/product/267/31560)，则拉流 URL 格式为 **`webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx`**。腾讯云直播拉流 URL 生成请参见 [获取播放地址](#step4)。

>? 如果需要拉不同分辨率、码率的流，可以拉转码流，转码流 URL 生成请参见 [直播转封装及转码](https://intl.cloud.tencent.com/document/product/267/31561)。

[](id:b_frame)
### 关于 B 帧
快直播 Web 方案**不支持 B 帧解码播放**，所以如果原始流存在 B 帧，则后台会自动进行转码去掉 B 帧，但这样会引入额外的转码延迟，并且会**产生转码费用**。建议尽量不推包含 B 帧的流，用户可以通过调整推流端软件（如 OBS）的视频编码参数来去除 B 帧。如果使用 OBS 推流，可以通过设置，关闭 B 帧。如下图：
![](https://main.qcloudimg.com/raw/b28d5919589364e6a1f78d62e0b58c47.png)

[](id:a_transcoding)
### 关于音频转码
由于 Web 端浏览器拉流仅支持标准 WebRTC 协议，不支持 AAC 音频格式，需要将推流的 AAC 音频格式转化为 OPUS 音频格式播放，因此会产生 [音频转码](https://intl.cloud.tencent.com/document/product/267/39604) 费用。
