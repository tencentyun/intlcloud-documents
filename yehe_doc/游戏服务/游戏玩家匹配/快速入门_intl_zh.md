本文指导您如何快速上手使用**游戏玩家匹配 GPM** 服务。
## 步骤1：开通服务
首次登录 [GPM 控制台](https://console.cloud.tencent.com/gpm)，需申请 GPM 内测资格，通过内测申请后，账号将自动开通 GPM 服务。


## 步骤2（可选）：准备一个接收事件消息的地址

您需要准备一个 HTTP 或 HTTPS 的 URL 地址，用于接收来自 GPM 的事件消息推送。为了让数据传输更安全，建议您使用 HTTPS。

## 步骤3：创建规则

进入**规则管理**，在规则列表页点击创建。详情请参见 [创建规则](https://intl.cloud.tencent.com/document/product/1072/39202)。
![](https://main.qcloudimg.com/raw/ef3b98bfe79a9a8e84fd22f2913701c0.png)


## 步骤4：创建匹配

进入**匹配管理**，在匹配列表页点击创建。详情请参见 [创建匹配](https://intl.cloud.tencent.com/document/product/1072/39203)。
![](https://main.qcloudimg.com/raw/af24136b1c7f6c137f49f343adc8b7b1.png)

## 步骤5：发起匹配

调用 [发起匹配接口](https://cloud.tencent.com/document/product/1294/49491)，为玩家发起匹配。

