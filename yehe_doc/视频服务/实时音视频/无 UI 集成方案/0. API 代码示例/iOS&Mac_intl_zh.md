本文主要介绍如何快速运行腾讯云 TRTC-API-Example（iOS&Mac）。

## 环境要求
- Xcode 11.0及以上版本。
- 请确保您的项目已设置有效的开发者签名。
- Qt Creator 4.13.3（Mac）及以上版本。

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

### 步骤4：编译运行
使用 XCode（11.0及以上的版本）打开源码目录下的 TRTC-API-Example-OC.xcworkspace 工程，编译并运行 TRTC-API-Example 工程即可。


## 常见问题

### 1 两台手机同时运行工程，为什么看不到彼此的画面？
请确保两台手机在运行工程时使用的是不同的 UserID，TRTC 不支持同一个 UserID （除非 SDKAppID 不同）在两个终端同时使用。

### 2. 防火墙有什么限制？
由于 SDK 使用 UDP 协议进行音视频传输，所以在对 UDP 有拦截的办公网络下无法使用。如遇到类似问题，请参见 [应对公司防火墙限制](https://intl.cloud.tencent.com/document/product/647/35164) 排查并解决。
