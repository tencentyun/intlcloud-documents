[](id:LVB)
## 云直播 
[](id:LVB_OPEN)
### 如何开通云直播服务？
进入 [云直播管理控制台](https://console.cloud.tencent.com/live)，进入腾讯云直播服务开通页，查看相关协议并勾选 **同意**，单击 **申请开通** 即可开通云直播服务。
![](https://main.qcloudimg.com/raw/6e3a5b7794e6dacdd77a9ce818c56e21.png)。

[](id:LVB_PUSH_SECRECT)
### 如何开启流防盗链 KEY？
推流防盗链 KEY 是为了确保只有您的 App 用户才可以推流的安全保护手段，可随时按您的需要在直播管理控制台 [域名管理](https://console.cloud.tencent.com/live/domainmanage) 中修改，详细请参见 [播放鉴权配置](https://intl.cloud.tencent.com/document/product/267/31060)。

[](id:LVB_API_SECRECT)
### 如何通过 API 访问鉴权 KEY？

API 访问鉴权 KEY 是您的后台服务器在调用云直播相关的 [云 API 接口](https://intl.cloud.tencent.com/document/product/267/30760) 时需要用到的，目的是帮助腾讯云确认调用的合法性，API 访问鉴权 KEY 的获取请参见 [接口鉴权](https://intl.cloud.tencent.com/document/product/267/37447)。

[](id:LVB_EVENT_URL)
### 如何回调事件通知 URL？
腾讯云可以对一些直播事件配置回调，腾讯云服务会以 HTTP POST 的形式向您配置的地址发送通知，事件回调 URL 修改请参见 [回调配置](https://intl.cloud.tencent.com/document/product/267/31074)。

## 云点播
### 如何开通云点播服务？
只需要在 [云点播管理控制台](https://console.cloud.tencent.com/vod/overview) 开通即可以使用云点播服务，默认按照日结方式计费。

### 如何查询我的点播 APPID？
每个腾讯云账号均有一个唯一的 APPID 与之对应，其位于 [账号信息](https://console.cloud.tencent.com/developer) 中。


[](id:IM)
## 即时通信（IM）
[](id:IM_OPEN)
### 如何开通 IM 服务？
进入 [即时通信 IM 管理控制台](https://console.cloud.tencent.com/avc)。
新认证的腾讯云账号，即时通信 IM 的应用列表是空的，单击【添加新应用】并填写相关信息后，单击【确定】，即可创建一个新的应用。

>! 云直播控制台支持添加即时通信 IM 应用，您可通过登录【云直播控制台】>【直播SDK】>[【应用管理】](https://console.cloud.tencent.com/live/license/appmanage)，单击【创建应用】，填写应用名称和应用简介，单击【确认】即可创建一个新的应用。

[](id:IM_SDKAPPID)
### 什么是 SDK APPID？
它表示您在该腾讯云账号下的一款产品，如果您有多个产品，就对应有多个 SDKAPPID。


[](id:IM_ADMIN)
 ### 什么是 Administrator？
IM 提供了一套 [REST](https://intl.cloud.tencent.com/document/product/1047/34621) API 用于让您的后台服务器可以直接调用 IM 服务，例如建群、发送系统消息、把某个用于剔除群组等等，但 IM REST API 仅允许管理员进行调用，也就是需要一个管理员用户名（Administrator）和对应的密码 (UserSig)，具体使用过程请参见 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。


>? UserSig 是用户登录即时通信 IM 的密码，具体获取密钥方法请参见 [获取密钥](https://intl.cloud.tencent.com/document/product/1047/34385#obtaining-a-key)。


## 对象存储服务（COS）
### 如何开通对象存储服务？
新认证的腾讯云账号都可以立刻使用对象存储服务，只需要进入 [COS管理控制台](https://console.cloud.tencent.com/cos) ，单击【存储桶列表】>【创建存储桶】，填写相关信息后单击【确定】，即可成功创建一个存储桶，可开始启用存储桶。


### 什么是 Bucket（桶）？
Bucket 是一个略显技术化的名词，翻译成中文即“桶”的意思，您可以简单将它理解为**磁盘分区**的概念。例如，您在腾讯云购买了对象存储服务（COS），而在某商城购买了一块新的硬盘，在您向上面存储数据之前，一般会先对其进行分区和格式化。那么我们可以这样说，您在真实世界里的硬盘上建一个分区，就好比在腾讯云的 COS 里建一个 Bucket。

### 如何查询我的 Bucketname？
您在创建 Bucket 时所指定的名称即为您的一个 Bucketname，例如在4.1的例子中所指定的 `xiaozhibo` 即是一个 Bucketname。

### 如何查询我的 COS APPID、SecretId 和 SecretKey？
单击 COS 管理控制台的 [密钥管理](https://console.cloud.tencent.com/cos5/key) 页面单击【云 API 密钥】，即可获得相关信息。
COS APPID 与 SecretId 和 SecretKey 相互绑定，他们主要用于访问 COS 的 API，因为 COS 是一个对安全要求很高的云端服务，所以如果 API 没有传入正确的密钥，腾讯云会拒绝这些 API 请求。

## 云服务器（可选）
您可以使用您自己的服务器作为业务服务器部署后台脚本，不过推荐您使用腾讯云的云服务器部署后台脚本，更为专业和稳定，另外如果您选择腾讯云的云数据库作为分布式数据库，则必须搭配腾讯云的云服务器才能访问。
进入 [云服务器管理控制台](https://console.cloud.tencent.com/cvm/overview)，选择左侧栏【实例】，单击【新建】，将进入服务器购买页。

>? 选择服务器镜像时，推荐您从服务器市场中选择带有 Nginx + PHP + MYSQL 的 Linux 镜像。

后续操作按照指引即可，镜像安装完毕后即可使用云服务器。

## 云数据库（可选）
### 如何开通云数据库？
请参见 [购买指引](https://intl.cloud.tencent.com/document/product/236/5160)。

### 如何使用数据库？
请参见：
- [初始化 MySQL 数据库](https://intl.cloud.tencent.com/document/product/236/3128)。
- [访问 MySQL 数据库](https://intl.cloud.tencent.com/document/product/236/37788)。
- [管理 MySQL 数据库](https://intl.cloud.tencent.com/document/product/236/31898)。
