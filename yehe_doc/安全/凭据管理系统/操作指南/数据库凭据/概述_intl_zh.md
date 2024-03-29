目前云上产品的账号密码面临管理权限失当、账号密码长时间不变更、配置中的密钥信息是明文等问题，导致数字资产损失。针对于这些风险，**数据库凭据**对凭据进行定期轮换，自动创建高强度密码和管理敏感配置信息，在降低账号的风险与安全威胁时，也能提高业务数据的安全性。

## 主要功能
- 凭据管理系统 SSM 与控制台集成，接管数据库账号的申请和分发功能。
- 结合腾讯 [密钥管理系统 KMS](https://intl.cloud.tencent.com/product/kms) 为敏感信息配置加密保护。
- 凭据管理系统 SSM 自动创建高强度密码，并对密码进行定期的修改与轮换。
- 灵活设置自动轮转的周期。

## 产品的架构
![](https://main.qcloudimg.com/raw/93b5e7074a63ca3a9f818254f6994a88.png)

#### 流程说明
1. 管理员创建数据库实例，设置数据库的账号、密码。
2. 管理员在凭据管理系统 SSM 中创建一个数据库凭据对象。
 - 授权 凭据管理系统 SSM 访问 MySQL 管理服务。
 - 设置数据库用户名前缀等。
 - 配置自动轮转的策略。
3. 当应用系统需要访问数据库时，可向凭据管理系统 SSM 请求访问凭据，接口请求详情，请参见 [获取凭据明文](https://intl.cloud.tencent.com/document/product/1078/38649)。
4. 应用系统通过访问凭据接口所返回的内容，解析出明文凭据，并获取到账号和密码，从而访问该用户对应的目标数据库。

## 使用限制

自动凭据轮换目前支持 **云数据库 MySQL** 和 **TDSQL MySQL版** 。

## 使用指引
- [创建数据库凭据](https://intl.cloud.tencent.com/document/product/1078/41801)
- [编辑数据库凭据](https://intl.cloud.tencent.com/document/product/1078/41802)
- [删除数据库凭据](https://intl.cloud.tencent.com/document/product/1078/41804)
- [访问控制](https://intl.cloud.tencent.com/document/product/1078/38610)
