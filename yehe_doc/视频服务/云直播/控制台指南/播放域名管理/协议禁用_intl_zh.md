通过对当前域名的播放协议进行限制，开启禁用后，该域名下对应的播放协议将无法使用，禁用协议生成的播放地址请求会被拒绝。

## 前提条件
- 已开通云直播服务，并登录 [云直播控制台](https://console.cloud.tencent.com/live/livestat)。
- 已添加 [播放域名](https://intl.cloud.tencent.com/document/product/267/35970)。


## 配置协议禁用
1. 选择 [域名管理](https://console.cloud.tencent.com/live/domainmanage)，单击需要配置 协议禁用的**播放域名**或右侧的**管理**，进入域名管理页。
2. 在**访问控制** > **协议禁用**中，支持对 RTMP、FLV、HLS 和 WebRTC 开启协议禁用。
3. 单击 **编辑** 按钮，在协议禁用配置中对指定协议开启协议禁用按钮。
4. 单击 **保存** ，即可保存配置。

![](https://qcloudimg.tencent-cloud.cn/raw/362960a0beaf910fa931fc173b1e8abd.png)

>!
>- 开启协议禁用需要一定时间，若协议禁用还在生效中，请在其他协议禁用生效后操作。
>- 正在播放中的流不受影响，禁用仅针对新流，除了 HLS 协议。



## 关闭协议禁用
对指定协议开启协议禁用后，若您需关闭此功能，具体操作如下：
1.选择 [域名管理](https://console.cloud.tencent.com/live/domainmanage)，单击需关闭协议禁用的**播放域名**或右侧的**管理**，进入域名管理页。
2.在**访问控制> 协议禁用**中，单击 **编辑** 按钮，在协议禁用配置中对指定协议关闭协议禁用按钮。
3.单击 **保存** ，即可保存配置。
![](https://qcloudimg.tencent-cloud.cn/raw/b3f339756306a55b39ed1acf1743c8c6.png)
