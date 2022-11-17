本文主要介绍如何快速运行腾讯云 TRTC Web SDK Demo。
## 准备工作
运行 TRTC Web SDK Demo 之前需要了解的事项。

### 支持的平台
TRTC Web SDK 基于 WebRTC 实现，目前支持桌面端和移动端的主流浏览器，详细支持度表格请参见 [支持的平台](https://intl.cloud.tencent.com/document/product/647/41664)。
如果您的应用场景不在支持的表格里，可以打开 [TRTC Web SDK 能力检测页面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 检测当前环境是否支持 WebRTC 所有能力，例如 WebView 等环境。

如果您的应用场景主要为教育场景，那么教师端推荐使用 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 解决方案，支持大小双路画面，更灵活的屏幕分享方案以及更强大的弱网络恢复能力。 

### URL 域名协议限制
由于浏览器安全策略的限制，使用 WebRTC 能力对页面的访问协议有严格的要求，请参照以下表格进行开发和部署应用。

| 应用场景     | 协议             | 接收（播放） | 发送（上麦） | 屏幕分享 | 备注     |
|----------|:-----------------|:---------|----------|--------|----------|
| 生产环境     | HTTPS 协议       | 支持       | 支持       | 支持     | **推荐** |
| 生产环境     | HTTP 协议        | 支持       | 不支持     | 不支持   |    -      |
| 本地开发环境 | http://localhost | 支持       | 支持       | 支持     | **推荐** |
| 本地开发环境 | http://127.0.0.1 | 支持       | 支持       | 支持     |      -    |
| 本地开发环境 | http://[本机IP]  | 支持       | 不支持     | 不支持   |    -      |
| 本地开发环境 | file:///         | 支持       | 支持       | 支持     |     -     |

### 防火墙限制
在使用 TRTC Web SDK 时，用户可能因防火墙限制导致无法正常进行音视频通话，请参考 [应对防火墙限制相关](https://www.tencentcloud.com/document/product/647/35164) 将相应端口及域名添加至防火墙白名单中。


## 前提条件
您已 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号。

## 操作步骤

### 步骤1：创建新的应用

1. 登录实时音视频控制台，选择【[应用管理](https://console.tencentcloud.com/trtc/app)】。

2. 单击【创建应用】输入应用名称，例如 `APIExample`；若您已创建过应用，可以勾选【选择已有应用】，然后单击【下一步】。
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### 步骤2：下载示例代码

1. 选择无 UI 集成后，然后您可以根据自己的业务平台，前往 Github 下载对应平台的示例代码。
2. 下载完成后，单击【下一步】。
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### 步骤3：配置工程
1. 在示例工程跑通阶段，选择【调试阶段】即可，然后记录下您的SDKAppID、Secret key。
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 打开下载完成的示例代码，根据图中指示找到，对应的文件位置，修改为您的SDKAppID、Secret key，此时工程配置已经完成，您可以单击【下一步】，

>?
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TRTC-API-Example 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/647/35166)。


## 常见问题

### 1. 出现客户端错误：“RtcError: no valid ice candidate found”该如何处理？
出现该错误说明 TRTC Web SDK 在 STUN 打洞失败，请根据 [应对防火墙限制相关](https://www.tencentcloud.com/document/product/647/35164) 检查防火墙配置。

### 2. 出现客户端错误："RtcError: ICE/DTLS Transport connection failed" 或 “RtcError: DTLS Transport connection timeout”该如何处理？
出现该错误说明 TRTC Web SDK 在建立媒体传输通道时失败，请根据 [应对防火墙限制相关](https://www.tencentcloud.com/document/product/647/35164) 检查防火墙配置。

### 3. 出现10006 error 该如何处理？
如果出现"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"，请确认您的实时音视频应用的服务状态是否为正常状态。
登录 [实时音视频控制台](https://console.cloud.tencent.com/rav)，单击您创建的应用，单击 **应用信息**，在应用信息面板即可确认服务状态。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? 其他常见问题参见 [Web 端相关](https://intl.cloud.tencent.com/document/product/647/37340)。
