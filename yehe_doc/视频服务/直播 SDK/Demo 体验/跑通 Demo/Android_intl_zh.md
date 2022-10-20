本文主要介绍如何快速运行腾讯云 MLVB-API-Example（Android）。

## 环境要求
- 最低兼容 Android 4.1（SDK API Level 16），建议使用 Android 5.0 （SDK API Level 21）及以上版本。
- Android Studio 3.5 及以上版本。
- App 要求 Android 4.1 及以上设备。

## 前提条件
您已 [注册腾讯云](https://www.tencentcloud.com/document/product/378/17985) 账号。

## 操作步骤
[](id:step1)
### 步骤一：下载 SDK 和 MLVB-API-Example 源码
1. 根据实际业务需求 [下载](https://www.tencentcloud.com/document/product/1071/38150) 相应的压缩包，这里以 [Professional](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip) 为例。
2. 下载完成后，解压。<br>
>! 源码也可以从 [Github](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example) 获得。

[](id:step2)
### 步骤二：配置 License
1. 登录 [云直播控制台](https://console.tencentcloud.com/live/livestat)，在左侧菜单中选择 **直播 SDK** >[ **License 管理**](https://console.tencentcloud.com/live/license)，单击**创建License**。 
![](https://qcloudimg.tencent-cloud.cn/raw/ed8480080cbbd5283d5f8bca8266304b.png) 
2. 根据实际需求填写 `App Name`、`Package Name` 和 `Bundle ID`，勾选功能模块 **直播**（直播推流 + 视频播放），单击**确定**。 
  - **Package Name**：请在App目录下的 **build.gradle** 文件查看 **applicationId** 。
  - **Bundle ID**：请在 **xcode** 中查看项目的 **Bundle Identifier** 。

3. License 成功创建后，页面会显示生成的 License 信息。**在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。** 
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png" width=800>
4. 打开 `LiteAVSDK_Professional_Android版本号/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` 文件，设置 `GenerateTestUserSig.java` 文件中的相关参数：
  - LICENSEURL：默认为 PLACEHOLDER，请设置为您的下载 Licence url。
  - LICENSEURLKEY：默认为 PLACEHOLDER，请设置为您的下载 Licence key。

[](id:step3)
### 步骤三：配置推流/播放能力
1. 在 [域名注册](https://dnspod.cloud.tencent.com/?from=qcloudProductDns) 申请域名，并备案成功。
2. 在 **云直播控制台** > **[域名管理](https://console.cloud.tencent.com/live/domainmanage)** 中添加推流/播放域名，具体操作请参见 [添加自有域名](https://intl.cloud.tencent.com/document/product/267/35970)。
3. 成功 [配置域名 CNAME](https://intl.cloud.tencent.com/document/product/267/31057)。
4. 配置好推流/播放域名后，在推流/播放域名的 **基本信息** 页面可以获得 `CNAME` 信息。
<img src="https://qcloudimg.tencent-cloud.cn/raw/3e43f156dce4b4575bdc6f4d6fdd87b6.png" width=500px>
5. 打开 `LiteAVSDK_Professional_Android版本号/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` 文件。
设置 `GenerateTestUserSig.java` 文件中的相关参数：
  - **PUSH_DOMAIN**：请设置为您的 [推流域名](https://console.cloud.tencent.com/live/domainmanage)。
  - **PLAY_DOMAIN**：请设置为您的 [播放域名](https://console.cloud.tencent.com/live/domainmanage)。
  - **LIVE_URL_KEY**：非必需，用于生成 txSecret 等鉴权信息，具体计算请参见 [推拉流 URL](https://cloud.tencent.com/document/product/454/7915)，查询步骤参见 [域名页面](https://console.cloud.tencent.com/live/domainmanage) > **管理** > **推流配置** > **鉴权配置**。<br>


[](id:push)
#### 配置推流参数
1. 找到并打开 `LiteAVSDK_Professional_Android版本号/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java` 文件。
2. 根据上面服务开通设置 [GenerateTestUserSig.java](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example/Debug/src/main/java/com/tencent/mlvb/debug/GenerateTestUserSig.java) 文件中的相关参数：
  - SDKAPPID：默认为 PLACEHOLDER，请设置为实际的 SDKAppID。
  - SECRETKEY：默认为 PLACEHOLDER，请设置为实际的密钥信息。

[](id:pushurl)
#### 推流 URL 字段说明
具体的推拉流 URL 字符串，需要开发者按照对应的协议自行拼接，拼装方案请参见 [推拉流 URL](https://www.tencentcloud.com/document/product/1071/39359)。Demo 中已经拼接好，运行后即可播放。

[](id:step5)
### 步骤五：编译运行
使用 Android Studio（3.5及以上的版本）打开源码工程 `MLVB-API-Example`，单击 **运行** 即可。
<img src="https://qcloudimg.tencent-cloud.cn/raw/70bb721a8cea4c41b697804cad70ed5b.png" width=300px>
