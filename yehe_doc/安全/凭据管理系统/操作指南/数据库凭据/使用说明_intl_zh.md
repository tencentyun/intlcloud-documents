## 前提条件
- 已创建数据库凭据，对于未创建数据库凭据的情况，可查阅 [创建数据库凭据](https://intl.cloud.tencent.com/document/product/1078/41801) 进行创建。
- 凭据已开启轮转，对未开启凭据轮转的情况，可查阅 [启用数据库凭据](https://intl.cloud.tencent.com/document/product/1078/41803) 开启轮转。



## 轮转的实现效果
SSM 会根据用户预先设定的轮转周期，对凭据中保存的账号密码信息进行更新。客户端通过调用 [获取凭据明文](https://intl.cloud.tencent.com/document/product/1078/38649) 可以获取到最新的有效账号和密码信息。
同一个凭据的账号和密码信息会发生变化，但对应的数据库的访问权限是相同的，SSM 会负责在数据库中同步创建或更新具有相同权限的账号或密码。

## 应用程序与SSM的集成
应用程序只需要通过调用 [获取凭据明文](https://intl.cloud.tencent.com/document/product/1078/38649)， 即可获取访问数据库最新的有效账号和密码信息，即可用于数据库的访问。

## 风险提示
### 风险点
SSM 在对数据库凭据进行周期性轮转时，会更新账号的密码，导致使用过期密码的账号访问数据库失败。

### 应对方案
为了防止访问数据库失败的情况发生，**请不要在客户端自动保存密码信息和使用带有数据库连接池功能的第三方 SDK**。请使用**最佳实践**中推荐的腾讯云官方提供的 **SSM SDK**（ [Go](https://github.com/TencentCloud/ssm-rotation-sdk-golang) 和 [Python](https://github.com/TencentCloud/ssm-rotation-sdk-python) ） 来连接数据库。 
