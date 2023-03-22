频道输入是StreamLive的媒体流输入通道，通常关联一个安全组和一个StreamLive的频道。

## 前提条件
- 已开通 [StreamLive](https://www.tencentcloud.com/products/mdl)。 
- 已登录 [StreamLive控制台](https://console.intl.cloud.tencent.com/mdl/input)。

## Input管理
单击左侧导航栏**Input Management**，可以查看已创建的input名称、类型、绑定状态、ID等信息。每一个Input通常可以关联一个安全组和一个StreamLive频道，被频道关联的Input状态会显示attached。每一个Input有A、B两个通道，是两个物理隔离的通道，对应频道两个通道，可同时推流，保障上行可用性。

![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


## 创建Input
频道输入提供PULL和PUSH两种输入方式。若您需要创建Input，单击页面左上角【Create Input】按钮，在弹窗中进行配置：
![](https://qcloudimg.tencent-cloud.cn/raw/0a58997dcc3241c77a07a05a458569c4.png)

- **Name**：Input名称，可由用户自定义。可支持1-32位数字、大小字母、下划线“_”。
- **Type**：Input类型，目前支持RTMP_PUSH、RTP_PUSH、RTP-FEC_PUSH、UDP_PUSH、SRT_PUSH、RTMP_PULL、HLS_PULL、MP4_PULL、RTSP_PULL、SRT_PULL等协议。
- **Security Group**：若是PUSH输入类型，则需要绑定Input安全组做安全校验。

##### Type：RTMP_PUSH
若Type选RTMP_PUSH，需要填Destination，分别是application name和stream name。
![](https://qcloudimg.tencent-cloud.cn/raw/0f449d8038bed66bcada1faa0481c92c.png)

##### Type：SRT_PUSH
若Type选SRT_PUSH，Destination代表streamid，非必填。
![](https://qcloudimg.tencent-cloud.cn/raw/f4a9ec18c0de6d127fce99d8c91aad89.png)

##### Type：PULL
若Type选PULL类型，需要填InputAddress，作为PULL的源。
![](https://qcloudimg.tencent-cloud.cn/raw/28291755993b3efb3b3bdd4b63bfd40d.png)


## 修改Input
若您需要修改Input，单击需要修改的Input右侧**Edit**，在弹窗中进行修改，修改完成后点击**Confirm**完成修改。
![](https://qcloudimg.tencent-cloud.cn/raw/45f415840a5b45d0a97baa965f05a45c.png)

## 删除Input
若您需要删除Input，单击需要删除的Input右侧**Delete**，在弹窗中点击**Confirm**完成删除。
![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


>! 
>- 控制台默认只支持最多5个input的存在。
>- 输入的媒体源目前至少需要包含一个视频数据通道。
>- 当使用MPEG-TS多路复用通道时，最多允许8路通道同时传输。

