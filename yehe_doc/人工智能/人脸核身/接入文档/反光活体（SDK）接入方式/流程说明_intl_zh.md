
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
![图1](https://qcloudimg.tencent-cloud.cn/raw/f963c590fc88067f81da0b7ca3df50f8.png)

相关后台接口：[GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646)，[DetectReflectLivenessAndCompare](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
## 时序图（详）

实际使用时，后台的接口需要传入URL，具体使用和原因可以见[如何传递资源](https://www.tencentcloud.com/document/product/1061/46849) 。
*CreateUploadUrl在图中将作为一个独立的参与角色*
![图2](https://qcloudimg.tencent-cloud.cn/raw/491abd12442624139fef0b39959a6745.png)
相关后台接口：[GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646)，[DetectReflectLivenessAndCompare](https://intl.cloud.tencent.com/zh/document/product/1061/44246)，[CreateUploadUrl](https://www.tencentcloud.com/document/product/1061/47648)
