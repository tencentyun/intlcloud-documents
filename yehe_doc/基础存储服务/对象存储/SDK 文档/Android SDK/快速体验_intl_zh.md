## 背景
移动互联网时代，App 作为移动互联网服务的基础设施，往往需要上传和下载大量的数据，数据的安全性和可靠性尤为重要。现在开发者可以将数据存储相关的问题交给 [腾讯云对象存储（Cloud Object Storage，COS）服务](https://intl.cloud.tencent.com/product/cos)，而只需要关心自己应用的业务逻辑即可，可减少很多工作量，提升开发效率。本文主要介绍如何快速搭建一个基于 COS 的应用传输服务，在腾讯云 COS 上实现应用数据的上传下载，在您的服务器上只需要部署您自己的业务、生成和管理临时密钥。

腾讯云 COS 提供 XML 版本的体验 demo，您可以参照本文档来体验 COS 传输实践 demo。

## 相关资源

本文涉及的 Demo 都存放在 [Github 仓库](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice)，用户可前往获取。

## 准备工作
- Android 系统版本：4.4 及以上。
- 腾讯云 APPID、SecretId、SecretKey（可在云 [API 密钥](https://console.cloud.tencent.com/capi) 中获取）。

## 搭建用户客户端

### 配置客户端

1. 在 [Github 仓库 ](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice) 下载项目文件，然后用 IDE 打开。
2. 在环境变量中配置您的 APPID、SecretId、SecretKey。
3. 运行项目，体验 COS 传输实践 demo。

>!
>- SecretId、SecretKey 明文不要暴露到不安全环境下。
>- 本项目采用的 ShortTimeCredentialProvider 仅仅是为了演示，正式环境中请不要采用此方式，建议采用 [通过临时密钥进行授权](https://intl.cloud.tencent.com/document/product/436/12159) 的方式。
>- 环境变量更改后，Android Studio 可能需要重启，相关配置才会更新生效。

### 运行示例 Demo

#### 查询存储桶列表
启动示例 App 后，将展示用户已创建的所有存储桶。

#### 创建存储桶
点击右上角**新建桶**，在配置页面输入桶名称并选择存储桶的所属 [地域](https://intl.cloud.tencent.com/document/product/436/6224)。

#### 查询对象列表

选择点击某个存储桶，将看到该存储桶内所有文件以及文件夹。

#### 上传文件
在文件列表页面点击右上角的**上传**，然后选择文件进行上传。

#### 下载文件
在对象列表中，点击文件下方的**下载**按钮，即可下载文件。
