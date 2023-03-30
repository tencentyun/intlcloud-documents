- 本文介绍带 UI 的 Web 端直播互动组件 TUIPusher & TUIPlayer。TUIPusher & TUIPlayer 集成  [即时通信 IM](https://intl.cloud.tencent.com/product/im)  、[实时音视频 TRTC](https://intl.cloud.tencent.com/product/trtc)等基础 SDK，为企业直播、电商带货、行业培训、远程教学等多种直播场景提供快速上线 Web 端直播推拉流工具的解决方案。

  TUIPusher & TUIPlayer 的优势：
  + 贴合直播场景需求，提供了含 UI 的直播场景通用解决方案，覆盖了直播场景常见功能（如设备选择、美颜、直播推流、观众拉流、聊天等），助力业务快速上线；
  + 直接接入腾讯云实时音视频 TRTC、腾讯云即时通信 IM 以及腾讯云超级播放器 TCPlayer 等基础 SDK，方便客户灵活扩展业务功能；
  + Web 端易于用户使用，易于功能迭代的天然优势；

  ## 快速体验

  TUIPusher 及 TUIPlayer 功能演示请看下图。同时，为了方便您快速体验 TUIPusher & TUIPlayer 的功能，我们结合用户管理系统和房间管理系统提供了 [TUIPusher 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/login.html) 及 [TUIPlayer 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/login.html)。
  >! 同时体验 TUIPusher 和 TUIPlayer 需要使用两个不同的账号登录。  

  ![TUIPusher演示](https://qcloudimg.tencent-cloud.cn/raw/8d33df705c07c80d75ad19096e681903.png)
  ![TUIPlayer演示](https://qcloudimg.tencent-cloud.cn/raw/6490fdf7db4980db3a98b4b103fb52f1.png)

  ## 代码下载

  Web 端直播互动组件（TUIPusher & TUIPlayer）下载方式如下：
  + [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) 
  + [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer)


  ## 功能介绍
  ### TUIPusher 推流组件
  - 支持采集摄像头和麦克风的流并推流
    - 可根据需求设置视频参数（帧率，分辨率，码率）
    - 支持开启美颜并设置视频美颜参数
  - 支持采集屏幕分享流并推流
  - 支持推流到腾讯云实时音视频后台，推流到腾讯云 CDN
  - 支持在线聊天室，和在线观众进行聊天互动
  - 支持获取观众列表，对在线观众进行禁言操作

  ### TUIPlayer 拉流组件
  - 支持同时播放音视频流和屏幕分享流
  - 支持在线聊天室，和主播及其他观众进行聊天互动
  - 支持超低延时直播（300ms 延时）, 快直播（1000ms 以内延时）以及标准直播（支持超高并发观看）三种拉流线路
  - 兼容桌面浏览器及移动端浏览器，支持移动端浏览器横屏观看
  >! 部分浏览器不支持 WebRTC，只能使用标准直播线路观看，如需体验其他线路，请尝试更换浏览器。

  ## 接入方式
  ### 注意事项
  - TUIPusher & TUIPlayer 基于腾讯云实时音视频和即时通信服务进行开发。实时音视频 TRTC 应用与 即时通信 IM 应用的 SDKAppID 一致，才能复用账号与鉴权。
  - 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦 SECRETKEY 泄露，攻击者就可以盗用您的腾讯云流量。正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

  ### 步骤一：开通腾讯云服务
  <dx-tabs>
  ::: 方式1：基于即时通信\sIM
  #### 步骤1：创建即时通信 IM 应用
  1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击 **创建新应用** 将弹出对话框。
  ![](https://qcloudimg.tencent-cloud.cn/raw/7382cbcd81df7afbad1e9af641697c87.png)
  2. 输入您的应用名称，单击 **确认** 即可完成创建。
  ![](https://qcloudimg.tencent-cloud.cn/raw/b3a630da00564cf7ef4a91b8492b646e.png)
  3. 您可在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 总览页面查看新建应用的状态、业务版本、SDKAppID、创建时间以及到期时间。请记录 SDKAppID 信息。

  #### 步骤2：获取 IM 密钥并开通实时音视频服务
  1. 在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 总览页单击您创建完成的即时通信 IM 应用，随即跳转至该应用的基础配置页。在 **基本信息** 区域，单击 **显示密钥**，复制并保存密钥信息。
  ![](https://qcloudimg.tencent-cloud.cn/raw/6f284cf687e9648d209567ed32983c84.png)
  >!请妥善保管密钥信息，谨防泄露。
  2. 在该应用的基础配置页，开通腾讯云实时音视频服务。
  ![](https://qcloudimg.tencent-cloud.cn/raw/8a9d1ca2c395fc6ebd26298a0f5226c4.png)
  :::
  ::: 方式2：基于实时音视频
  [](id:step1)
  #### 步骤1：创建实时音视频 TRTC 应用
  1. [注册腾讯云账号](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) 并开通 [实时音视频](https://console.cloud.tencent.com/trtc) 和 [即时通信](https://console.cloud.tencent.com/im) 服务。
  2. 在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 单击 **应用管理 > 创建应用** 创建新应用。
  ![创建应用](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)

  #### 步骤2: 获取 TRTC 密钥信息
  1. 在 **应用管理 > 应用信息** 中获取 SDKAppID 信息。
  ![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)
  2. 在 **应用管理 > 快速上手** 中获取应用的 secretKey 信息。
  ![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)

  <dx-alert infotype="explain">
  - 首次创建实时音视频应用的腾讯云账号，可获赠一个10000分钟的音视频资源免费试用包。
  - 创建实时音视频应用之后会自动创建一个 SDKAppID 相同的即时通信 IM 应用，可在 [即时通信控制台](https://console.cloud.tencent.com/im) 配置该应用的套餐信息。</dx-alert>

  :::
  </dx-tabs>

  [](id:step2)
  ### 步骤二：项目准备

  1. 在 [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web) 下载 TUIPusher & TUIPlayer 代码。
  2. 为 TUIPusher & TUIPlayer 安装依赖。
  ```bash
  cd Web/TUIPusher
  npm install
  
  cd Web/TUIPlayer
  npm install
  ```
  3. 将 sdkAppId 和 secretKey 填入 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中。
  ![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
  4. 本地开发环境运行 TUIPusher & TUIPlayer。
  ```bash
  cd Web/TUIPusher
  npm run serve
  
  cd Web/TUIPlayer
  npm run serve
  ```
  5. 可打开 `http://localhost:8080` 和 `http://localhost:8081` 体验 TUIPusher 和 TUIPlayer 功能。
  6. 可更改 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中的房间，主播及观众等信息，**注意保持 TUIPusher 和 TUIPlayer 的房间信息，主播信息一致**。

  >!
  >- 完成以上配置，您可以使用 TUIPusher & TUIPlayer 进行超低延时直播，如您需要支持快直播和标准直播，请继续阅读 [步骤三：旁路直播](#step3)。
  >- 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦您的 `SECRETKEY` 泄露，攻击者就可以盗用您的腾讯云流量。
  >- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

  [](id:step3)
  ### 步骤三：旁路直播

  TUIPusher & TUIPlayer 实现的快直播和标准直播依托于腾讯云 [云直播服务](https://intl.cloud.tencent.com/document/product/267)，因此支持快直播和标准直播线路需要您开启旁路推流功能。

  1. 在 [**实时音视频控制台**](https://console.cloud.tencent.com/trtc) 中为您正在使用的应用开启旁路推流配置，可按需开启指定流旁路或全局自动旁路。 
  ![](https://qcloudimg.tencent-cloud.cn/raw/b65584a5b096481ade6e302dabedcd5f.png)
  2. 请在 [**域名管理**](https://console.cloud.tencent.com/live/domainmanage) 页面添加自有播放域名，具体请参见 [添加自有域名](https://intl.cloud.tencent.com/document/product/267/35970)。
  3. 在 `TUIPlayer/src/config/basic-info-config.js` 配置文件中配置播放域名。

  完成以上配置，您可以体验 TUIPusher & TUIPlayer 支持超低延时直播，快直播以及标准直播的所有功能。

  [](id:step4)
  ### 步骤四：生产环境应用

  当您将 TUIPusher & TUIPlayer 用于生产应用时，在接入 TUIPusher & TUIPlayer 之外，您需要：

  - 创建用户管理系统，用于管理产品用户信息，包括但不限于用户 ID，用户名，用户头像等。
  - 创建房间管理系统，用于管理产品直播间信息，包括但不限于直播间 ID、直播间名称，直播间主播信息等。
  - 服务端生成 UserSig。
  > !
  > - 本文生成 UserSig 的方式，是在客户端根据您填入的 sdkAppId 及 secretKey 生成 userSig，该方式的 secretKey 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TUIPusher & TUIPlayer 进行功能调试**。
  > - 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的应用向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。
  - 参考 `TUIPusher/src/pusher.vue` 及 `TUIPlayer/src/player.vue` 文件，将用户信息、直播间信息、SDKAppId 及 UserSig 等账号信息提交到 vuex 的 store 进行全局存储，您就可以跑通推拉流两个客户端的所有功能。详细业务流程参见下图：
  ![](https://qcloudimg.tencent-cloud.cn/raw/30e959d1b4605532f6d4cac190cdd1df.png)

  ## 相关问题
  ### Web 端如何实现美颜功能？
  请参见 [开启美颜](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)。

  ### Web 端如何实现屏幕共享？
  请参见 [屏幕分享](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)。

  ### Web 端如何实现云端录制?
  1. 开启**云端录制**功能，具体操作请参见 [实现云端录制与回放](https://intl.cloud.tencent.com/document/product/647/35426)。
  2. 开启**云端录制**> **指定用户录制**之后，Web 端可通过在调用 [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) 接口时传入 userDefineRecordId 参数开启录制。

  ### Web 端如何实现推流到 CDN ？
  Web 端推流到 CDN 请参见 [实现推流到 CDN](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)。

  ### Web 端如何实现快直播拉流？
  实现快直播拉流的方式是通过 Web SDK 推流到 CDN 之后使用 WebRTC 协议拉流。

  ## 注意事项
  ### 平台支持

  | 操作系统 | 浏览器类型                   | 浏览器最低版本要求 | TUIPlayer                  | TUIPusher | TUIPusher 屏幕分享           |
  | :------- | :--------------------------- | :----------------- | :------------------------- | :-------- | :--------------------------- |
  | Mac OS   | 桌面版 Safari 浏览器         | 11+                | 支持                       | 支持      | 支持（需要 Safari13+ 版本）  |
  | Mac OS   | 桌面版 Chrome 浏览器         | 56+                | 支持                       | 支持      | 支持（需要 Chrome72+ 版本）  |
  | Mac OS   | 桌面版 Firefox 浏览器        | 56+                | 支持                       | 支持      | 支持（需要 Firefox66+ 版本） |
  | Mac OS   | 桌面版 Edge 浏览器           | 80+                | 支持                       | 支持      | 支持                         |
  | Mac OS   | 桌面版微信内嵌网页           | -                  | 支持                       | 不支持    | 不支持                       |
  | Mac OS   | 桌面版企业微信内嵌网页       | -                  | 支持                       | 不支持    | 不支持                       |
  | Windows  | 桌面版 Chrome 浏览器         | 56+                | 支持                       | 支持      | 支持（需要 Chrome72+ 版本）  |
  | Windows  | 桌面版 QQ 浏览器（极速内核） | 10.4+              | 支持                       | 支持      | 不支持                       |
  | Windows  | 桌面版 Firefox 浏览器        | 56+                | 支持                       | 支持      | 支持（需要 Firefox66+ 版本） |
  | Windows  | 桌面版 Edge 浏览器           | 80+                | 支持                       | 支持      | 支持                         |
  | Windows  | 桌面版微信内嵌网页           | -                  | 支持                       | 不支持    | 不支持                       |
  | Windows  | 桌面版企业微信内嵌网页       | -                  | 支持                       | 不支持    | 不支持                       |
  | iOS      | 微信内嵌浏览器               | -                  | 支持                       | 不支持    | 不支持                       |
  | iOS      | 企业微信内嵌浏览器           | -                  | 支持                       | 不支持    | 不支持                       |
  | iOS      | 移动版 Safari 浏览器         | -                  | 支持                       | 不支持    | 不支持                       |
  | iOS      | 移动版 Chrome 浏览器         | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 微信内嵌浏览器               | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 企业微信浏览器               | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 移动版 Chrome 浏览器         | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 移动版 QQ 浏览器             | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 移动版 Firefox 浏览器        | -                  | 支持                       | 不支持    | 不支持                       |
  | Android  | 移动端 UC 浏览器             | -                  | 支持（仅支持标准直播观看） | 不支持    | 不支持                       |

  ### 域名要求
  出于对用户安全、隐私等问题的考虑，浏览器限制网页在 HTTPS 协议下才能正常使用 TUIPusher & TUIPlayer 的全部功能。为确保生产环境用户顺畅接入和体验 TUIPusher & TUIPlayer 的全部功能，请使用 HTTPS 协议访问音视频应用页面。
  >! 本地开发可以通过 `http://localhost` 协议进行访问。

  URL 域名及协议支持情况请参考如下表格：

  | 应用场景     | 协议               | TUIPlayer | TUIPusher | TUIPusher 屏幕分享 | 备注 |
  | ------------ | ------------------ | --------- | --------- | ------------------ | ---- |
  | 生产环境     | HTTPS 协议         | 支持      | 支持      | 支持               | 推荐 |
  | 生产环境     | HTTP 协议          | 支持      | 不支持    | 不支持             | -    |
  | 本地开发环境 | `http://localhost` | 支持      | 支持      | 支持               | 推荐 |
  | 本地开发环境 | `http://127.0.0.1` | 支持      | 支持      | 支持               | -    |
  | 本地开发环境 | `http://[本机IP]`  | 支持      | 不支持    | 不支持             | -    |

  ### 防火墙限制
  TUIPusher & TUIPlayer 依赖以下端口进行数据传输，请将其加入防火墙白名单。
  - TCP 端口：8687
  - UDP 端口：8000，8080，8800，843，443，16285
  - 域名：qcloud.rtc.qq.com

  ## 结语
  在后续的迭代中, TRTC Web 端推拉流组件会逐渐与 iOS、Andriod 等各端连通，并在 Web 端实现观众连麦、高级美颜、自定义布局、转推多平台、上传图片文字音乐等能力，欢迎大家多多使用、提出您的宝贵意见。

  如果有任何需要或者反馈，可以联系：colleenyu@tencent.com。
