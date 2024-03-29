DRM 加密的证书管理功能由第三方服务商华曦达（SDMC）和DRMtoday提供，要访问华曦达证书管理或DRMtoday管理必须提供对应的用户密钥信息。本文主要说明如何在华曦达平台或DRMtoday平台获取用户密钥信息。

## 华曦达
### 操作步骤
1. 访问 [华曦达 SDMC DRM 服务](https://www.xmediacloud.com/contact-us/) 并进行注册。
![](https://qcloudimg.tencent-cloud.cn/raw/e92825b46f81fce995a115c0905915cb.png)
2. 按需填写完后，单击 **send message**，等待华曦达回复。消息发送成功后，过段时间（几小时），会收到系统邮件反馈。此后等待华曦达商务联系，确认些事项后会收到一个账号登录邮件。
![](https://qcloudimg.tencent-cloud.cn/raw/73ca49235b99ef7c42c97514a46f47c8.png)
3. 华曦达审核通过后会给您发送包含华曦达 DRM 控制台地址及登初始密码的邮件。
4. 登录 [华曦达 DRM 控制台](https://sso.multidrm.tv/login)，输入账号及密码即可登录成功。
![](https://qcloudimg.tencent-cloud.cn/raw/1833a48650c8ba607ad57701839b6d33.png)
5. 进入控制台单击 **DRM SETTING** ，获取用户密钥信息 UID、SecretID 及 SecretKey。
![](https://qcloudimg.tencent-cloud.cn/raw/59b1edb28e121521e9806b0d062b7495.png)
6. 获取 Access Secret 的用户 ID 及密码后，将用户密钥信息填至云直播 [DRM 管理](https://console.cloud.tencent.com/live/config/drm)。
![](https://qcloudimg.tencent-cloud.cn/raw/8b1e5a5214c518aa387157921cd9acf6.png)

## DRMtoday
### 操作步骤
1. 访问 [DRMtoday](https://castlabs.com/free-trials/drmtoday/) 并进行注册。
![](https://qcloudimg.tencent-cloud.cn/raw/e775679d700c980bf41e998af8d7fb25.png)
2. 按需填写完后，单击 **send** ，等待 drmtoday 回复。消息发送成功后，过段时间（几小时），会收到系统邮件反馈。此后等待一段时间后会收到一个账号登录邮件。
![](https://qcloudimg.tencent-cloud.cn/raw/dd40958e4ac33287ca764587cecdbe0a.png)
3. DRMtoday 审核通过后会给您发送包含 DRMtoda y登录地址及初始密码的邮件。
![](https://qcloudimg.tencent-cloud.cn/raw/6392ffb43cf33a2180aed06a3a8c51fa.png)
4. 登录 [DRMtoday](https://login.castlabs.com/login?response_type=code&client_id=1fc7irb6c3cumm1004dpv8fbs1&scope=openid%20profile%20email&state=bvqz7MJ1DQ4A-X_dzYZDflN3BT_O_jRF6OFxpL3fnvE%3D&redirect_uri=https://fe.staging.drmtoday.com/login/oauth2/code/&nonce=gVEoLbgH7RDiR-EXX6PiAvEgqx3UIg8fCBfDniiHZAY)，输入账号及密码即可登录成功。
![](https://qcloudimg.tencent-cloud.cn/raw/d5355f8f48e0f6056b89cdc0cb2ab108.png)
5. 进入控制页面 drmtoday。
![](https://qcloudimg.tencent-cloud.cn/raw/e6da9e6ff0b15e423f77ede1fbf69879.png)
6. 进入 API 界面，获取商户名称和商户的 uuid。 (merchantName\merchantUUID)
![](https://qcloudimg.tencent-cloud.cn/raw/e79ec6a6287cb6ae4ae646e312a88209.png)
7. 进入 Users 界面，新建API账号，赋予 API 账号及权限，记住密码。
>! 密码只闪现一次，需要记录下来。获取到 API 账号及密码。(merchantAPIname/merchantAPIpassword)

![](https://qcloudimg.tencent-cloud.cn/raw/48d71df6591557ff51d8dc911c9d60bf.png)
使能新建 API 账号：
![](https://qcloudimg.tencent-cloud.cn/raw/d59f5b5cbbaff1fcca550c6962ddaff8.png)
8. 进入 Configuration 中的 Ingest settings 加密密钥获取设置子界面。新建密钥种子，用来生成 key 和 iv。(keySeedID/ivSeedID)
>? 通过 key seed 生成密钥，可重复查询。可用于对接DRM加密厂商。(简单的 HMAC SHA512：使用 key seed 和 keyId 做 HMAC SHA512，生成加密串的前16位作为 key 或者 iv)。

![](https://qcloudimg.tencent-cloud.cn/raw/5fa20f0cd056e6e91cb8b4df7548ca5c.png)
9. 获取用户 merchantName、merchantUUID、merchantAPIname、merchantAPIpassword 及 keySeedID、ivSeedID 后，将用户信息填至云直播 DRM 管理。
![](https://qcloudimg.tencent-cloud.cn/raw/e648c01c8f7892252932ef8a7a6024c4.png)
>? 在您对接 DRM、华曦达和DRMtoday的过程中的任何问题，都可以提工单 [联系我们](https://console.cloud.tencent.com/workorder/category)，我们全程负责帮您解决。