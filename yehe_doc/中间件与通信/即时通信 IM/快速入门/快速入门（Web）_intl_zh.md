Web Demo 是基于 IM TUIKit 实现，TUIKit 中包含会话、聊天、群组、个人资料管理等功能，基于 TUIKit 您可以像搭积木一样快速搭建起自己的业务逻辑。

## 效果展示

### 会话管理

| 发起会话 | 会话列表 | 会话列表管理 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/562deec9715ae2c50f65e8d40c4d7cac.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/990204616a1c551c36ff5bdc57caa66c.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/695589f54d4ac0b9bb9bc24eb97c7e6d.png) |

### 聊天管理

| 消息列表 | 消息发送 | 群聊管理 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/8cb4fd0813a7ce0f3cab8468098dd896.png) |![](https://qcloudimg.tencent-cloud.cn/raw/f931993108c14ba3b2e628e4ed50a316.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/bb9b0449eb712f9e6fececfdb199418a.png) |

| 功能  | 说明  |
| --- | --- |
| 会话管理 | 1. 用于用户发起单人/多人会话<br/>2. 用于展示用户的会话列表<br/>3. 用于用户会话列表的管理 |
| 聊天管理 | 1. 用于消息列表的展示<br/>2. 用于消息发送<br/>3. 用于群聊管理 |


## 跑通步骤

### 步骤1：下载源码

根据您的实际业务需求，下载 SDK 及配套的 [Demo 源码](https://github.com/TencentCloud/TIMSDK)。

```shell
# 命令行执行
git clone https://github.com/TencentCloud/TIMSDK.git

# 进入 Web 项目

cd TIMSDK/Web/Demo

# 安装 demo 依赖
npm install

cd TIMSDK/Web/Demo/src/TUIKit

# 安装 TUIKit 依赖
npm install
```

### 步骤2：初始化
1. 打开终端目录的工程，找到对应的 GenerateTestUserSig 文件，路径为：/debug/GenerateTestUserSig.js。
2. 设置 GenerateTestUserSig 文件中的相关参数，其中 SDKAppID 和密钥等信息，可通过 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取，单击目标应用卡片，进入应用的基础配置页面。
3. ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
3. 在**基本信息**区域，单击**显示密钥**，复制并保存密钥信息至 GenerateTestUserSig 文件。



> !本文提到的获取 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 Demo 和功能调试**。 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

### 步骤3：启动项目

```shell
# 启动项目
npm run serve
```

- [SDK API 手册](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK 更新日志](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo 源码](https://github.com/TencentCloud/TIMSDK/tree/master/Web/Demo)
