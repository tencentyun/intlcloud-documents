本文档介绍如何判断子账号用户类型，且如何登录子账号。登录成功后，子账号可在权限范围内管理主账号下的资源。

## 子账号用户类型判断
子账号的类型分为子用户、协作者以及消息接收人，您可以通过以下两种方式判断所属类型：
- 根据 [用户类型](https://intl.cloud.tencent.com/document/product/598/32633) 文档中的表格说明判断账号类型。
- 联系主账号或者拥有 `cam:ListSubAccounts` 接口权限的子账号进入 [用户列表](https://console.cloud.tencent.com/cam) 控制台查看“用户类型”。

## 子账号登录
### 协作者登录
如果您的子账号用户类型是协作者，您可以使用您主账号身份关联的登录方式进入 [腾讯云账号登录](https://intl.cloud.tencent.com/login)  页面，选择协作者身份登录您的子账号，在权限范围内管理主账号下的资源。具体操作方式请参见 [协作者登录](https://intl.cloud.tencent.com/document/product/598/32659)。
### 子用户登录
- 子账号用户类型为**子用户**，您可以进入 [腾讯云子用户登录](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F598%2F36621) 页面输入主账号 ID、子用户名、登录密码信息进行子账号登录。详细请参见 [子用户登录](https://intl.cloud.tencent.com/document/product/598/34006)。

>?消息接收人仅可通过主账号设置的关联联系方式接收消息通知，无法通过编程访问或登录腾讯云控制台管理主账号下的资源。
