应用云渲染 PaaS 服务，帮助您实现应用云端运行，用户无需下载，即可通过视频流操作云上应用。
![](https://qcloudimg.tencent-cloud.cn/raw/6db9536d93dfad8c4a3113229b9144ce.jpg)

## 云 API
- **云 API：**云 API [3.0 版本](https://intl.cloud.tencent.com/product/api) 是腾讯云开放生态的基石，具备易于自动化、易于远程调用、兼容性强及对系统要求低等优势。通过云 API，您只需少量的代码即可快速操作云产品，针对频繁调用的功能可以提高效率。您还可将云 API 进行组合，实现更高级的功能。
- **访问密钥：**
访问密钥即云 API 密钥，是用户访问腾讯云 API 进行身份验证时需要用到的安全凭证，由 SecretId 和 SecretKey 一起组成。若用户还没有 API 密钥，则需要在 API 密钥管理中新建，否则就无法调用云 API 接口。访问密钥请在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 页面中获取。

## 运行环境
### 云端软件环境
- **部署条件**：您所提供的云应用安装包需要支持"绿色"部署安装，即应用的运行不需要依赖修改注册表等其他系统配置。
- **系统限制**：不支持调用 Windows 系统的 PowerShell 和 CMD 服务。
- **端口限制**：不支持端口监听，因为服务提供的外网 IP 是不固定的；不支持子网广播，如有相关需求建议通过公网方式获取。

### 云渲染服务环境
**网络条件**：应用云渲染服务网络依赖 UDP 数据收发，需要放开用户端所有来源 IP 使用 UDP 8000 端口限制，如无特殊安全问题，建议放开所有 UDP 端口限制。

## 接入服务能力
应用云渲染都是前后端一体的 PaaS 产品，提供后端 API 和各终端 SDK，您需要搭建自己的客户端程序以及后台服务，才能为您的用户提供服务。
![](https://qcloudimg.tencent-cloud.cn/raw/eddd4735374bf4605d1b233561c239aa.jpg)

- **后台 API：**
应用云渲染提供了业务所需调用的后台 [云 API](https://intl.cloud.tencent.com/document/product/1158/49958) ，通过云 API 您的业务后台可以完成请求您的并发资源以及创建会话等功能。
- **终端 SDK：**
应用云渲染提供各终端 SDK 用于支持 Android 端、iOS 端 以及 H5 平台接入。您的客户端需要集成终端 SDK。SDK 提供了丰富的接口，满足大部分接入需求。更多详情可参见应用云渲染终端 [JS SDK](https://intl.cloud.tencent.com/document/product/1158/49627)、[Android SDK](https://intl.cloud.tencent.com/document/product/1158/49628)、[iOS SDK](https://intl.cloud.tencent.com/document/product/1158/49629)。

