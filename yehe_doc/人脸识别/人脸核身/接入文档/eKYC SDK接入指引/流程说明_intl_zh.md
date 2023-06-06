## 接入准备
- 注册腾讯云账号并进入慧眼控制台[开通服务](https://console.intl.cloud.tencent.com/faceid) 
- [联系我们](https://www.tencentcloud.com/document/product/1061/52144)下载最新的[SDK](https://console.intl.cloud.tencent.com/faceid) 及[license](https://console.intl.cloud.tencent.com/faceid) 

## 名词介绍

- Customer APP: 客户自己开发的APP
- Customer Server: 客户自己的业务后台
- Tencent Cloud API: 腾讯云提供的后台接口，用于获取刷脸凭证并获取刷脸结果
- SDK: 腾讯云提供的Android或者iOS的SDK，用于集成入客户的APP并结合后台接口启动刷脸

## 时序图（简）

主要参与角色示意图如下

![](https://qcloudimg.tencent-cloud.cn/raw/728a228977a5c7bfa67d2a5af098722b.png)

相关后台接口：[ApplySdkVerificationToken](https://www.tencentcloud.com/document/product/1061/49954)，[GetSdkVerificationResult](https://www.tencentcloud.com/document/product/1061/49951)
