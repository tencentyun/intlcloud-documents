
MediaLive 支持直接联合腾讯云 MediaPackage 一起使用，将 HLS/DASH 格式直播流直接输出至同账号下的 MediaPackage 中，以便于用户形成自己的源站，从而进行下一步的视频分发与播放。
### 步骤1：开通 MediaPackage
在输出至 MediaPackage 前请先开通 MediaPackage 服务，登录[控制台](https://console.cloud.tencent.com/mdp/channel)并创建 Channel。
### 步骤2：完成 MediaPackage 的 Channel 创建
点击左上方 Create Channel 创建一个频道，填写频道的名称以及与 MediaLive 输出类型一致的协议。例如：当MediaLive 选择输出类型为 HLS_MediaPackage 时，则此处选择 HLS。
![](https://main.qcloudimg.com/raw/024c629fe57a6c3fd4761aadaf45a32e.jpg)

>! MediaLive 与 MediaPackage 需要处于同一 region 下。
>

### 步骤3：创建 endpoint
创建 channel 完毕后会进入到 channel 的详情页中，此时我们创建一个 endpoint 节点，您也可以根据业务实际需要选择是否开启 IP 黑白名单或者鉴权功能。
 ![](https://main.qcloudimg.com/raw/c3bce6fe0f437599c6acb5de6752c21f.jpg)

### 步骤4：获得 endpoint 地址及 Channel ID
创建完毕后的 endpoint 的 URL 即为播放/源站地址。
![](https://main.qcloudimg.com/raw/5b98c4ebc014ebaeb9acb56cf436f876.jpg)

>? Channel ID 将用于 MediaLive 输出的填写。
>

### 步骤5：选择输出类型为HLS_MEDIAPACKAGE或DASH_MEDIAPACKAGE
回到 MediaLive 控制台，在配置输出时，选择输出类型为 HLS_MEDIAPACKAGE 或者 DASH_MEDIAPACKAGE（这取决于您的业务实际需求及您刚刚创建的 MediaPackage 的 channel 类型）。再填入您 MediaPackage 中的 channel ID 即可。
![](https://main.qcloudimg.com/raw/a6716afaa492de5d744ca1ef03b4c1d5.jpg)

### 步骤6：保存并提交配置
此时您可回到 [MediaLive 频道创建](https://intl.cloud.tencent.com/document/product/1048/38374) 完成其余channel配置，并点击保存之后提交。
