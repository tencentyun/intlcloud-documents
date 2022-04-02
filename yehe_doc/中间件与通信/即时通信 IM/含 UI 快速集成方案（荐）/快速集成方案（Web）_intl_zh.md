Web Demo 是基于 IM SDK 实现的一套 UI 组件，其包含会话、聊天、搜索、关系链、群组、音视频通话等功能，基于 UI 组件您可以像搭积木一样快速搭建起自己的业务逻辑。

## 功能说明

| 功能 | 说明 |
|---------|---------|
| 搜索 | 主要用于搜索和展示会话或消息 |
| 会话 | 主要用于拉取和展示会话列表 |
| 聊天 | 主要用于收发和展示消息 |
| 关系链 | 主要用于拉取和展示好友列表 |
| 群组 | 主要用于拉取和展示群信息 |
| 音视频通话 | 主要用于音视频通话 |


## 操作步骤
[](id:step1)
### 步骤1：下载源码
根据您的实际业务需求，下载 SDK 及配套的 [Demo 源码](https://intl.cloud.tencent.com/document/product/1047/33996)。
<dx-codeblock>
:::  js

# 命令行执行
git clone https://github.com/tencentyun/TIMSDK.git

# 进入 Web 项目

cd TIMSDK/Web/Demo

# 安装依赖
npm install
:::
</dx-codeblock>

### 步骤2：初始化 Demo

1. 打开终端目录的工程，找到对应的 `GenerateTestUserSig` 文件，路径为：/public/debug/GenerateTestUserSig.js
2. 设置`GenerateTestUserSig`文件中的相关参数，其中 SDKAppID 和密钥等信息，可通过 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取，单击目标应用卡片，进入应用的基础配置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
3. 在**基本信息**区域，单击**显示密钥**，复制并保存密钥信息至 `GenerateTestUserSig` 文件。

>!本文提到的获取 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 Demo 和功能调试**。
>正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。


### 步骤3：集成静态资源文件
在自己的项目中集成静态资源文件（工具，图片等）。
  <img src="https://qcloudimg.tencent-cloud.cn/raw/f0aff5e265cac1d7eefab7fa53bda545.png"   width = "200">

### 步骤4：集成所需模块
1. 复制整个 components 到自己项目中：
![](https://qcloudimg.tencent-cloud.cn/raw/18a5f940d61cb15c3979cf6944152bb2.png)
2. 也可以只集成自己所需的模块，下面以会话模块为例：
![](https://qcloudimg.tencent-cloud.cn/raw/8b9573f02146f3958af080bd07f716eb.png)

### 步骤5：更新路由
根据引入模块更新路由：
  <img src="https://qcloudimg.tencent-cloud.cn/raw/38733003ae12c255d615897102149097.png"   width = "200">

## 参见文档

- [SDK API 手册](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK 更新日志](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo 源码](https://github.com/tencentyun/TIMSDK/tree/master/Web/Demo)

