## 操作场景
您可以通过跨账号访问角色生成的临时安全密钥使您的其它腾讯云账号扮演腾讯云已有账号的角色，在权限范围内管理腾讯云资源。
## 前提条件
拥有多个腾讯云主账号，如您当前没有腾讯云账号，可参考 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 创建您需要的账号。本文档中假设拥有两个腾讯云账号 A、B，假设 B 账号想管理账号 A 下的腾讯云资源。
## 操作步骤
1. [登录](https://intl.cloud.tencent.com/document/product/378/36004) 腾讯云账号 A ，在账号 A 下创建自定义角色。自定义角色创建请参阅 [为腾讯云主账号创建角色](https://intl.cloud.tencent.com/document/product/598/19381)。
2. 使用账号 B 的访问密钥通过 云 API 工具调用  [sts:AssumeRole](https://intl.cloud.tencent.com/document/product/598/35840) 生成临时安全密钥。
3. 使用步骤 2 生成的临时安全密钥扮演账号 A 的角色，在角色的权限范围内通过  云 API 工具 调用您需要的接口管理腾讯云资源即可。
