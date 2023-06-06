# 接入说明

## 接入准备
- 注册腾讯云账号并进入慧眼控制台[开通服务](https://console.intl.cloud.tencent.com/faceid) 

## 名词介绍

- Customer H5: 客户自己开发的H5
- Customer Server: 客户自己的业务后台
- Tencent Cloud API: 腾讯云提供的后台接口，用于获取刷脸凭证并获取刷脸结果
- Tencent Cloud H5: 腾讯云的核身页面

## 时序图（简）

![1](https://qcloudimg.tencent-cloud.cn/raw/f963c590fc88067f81da0b7ca3df50f8.png)

相关后台接口：[ApplyWebVerificationToken](https://intl.cloud.tencent.com/zh/document/product/1061/44246)，[GetWebVerificationResult](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
## 时序图（详）

实际使用时，后台获取token的接口需要传入比对图URL，具体使用和原因可以见[如何传递资源](https://console.intl.cloud.tencent.com/faceid) 。
*CreateUploadUrl在图中将作为一个独立的参与角色*

![2](https://qcloudimg.tencent-cloud.cn/raw/491abd12442624139fef0b39959a6745.png)

相关后台接口：[ApplyWebVerificationToken](https://intl.cloud.tencent.com/zh/document/product/1061/44246)，[GetWebVerificationResult](https://intl.cloud.tencent.com/zh/document/product/1061/44246)，[CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
