## 操作场景
TDSQL MySQL版 支持重置实例密码，如您在使用数据库过程中，忘记了数据库账号密码或需修改密码，可通过控制台重新设置密码。

>?为了数据安全，建议您定期更换密码，最长间隔不超过3个月。

## 操作步骤
1. 登录 [TDSQL 控制台](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)，在**实例列表**中，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**帐号管理**页，找到需要重置密码的帐号，选择**更多** > **重置密码**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yk5M998_11.png)
3. 在重置密码对话框，输入新密码和确认密码，单击**确定**。
>?为避免创建、修改、删除帐号信息给您的业务带来风险，建议配置 [访问管理](https://intl.cloud.tencent.com/document/product/1042/33343)，谨慎重置密码。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/z4ky065_12.png)

## 相关 API

| API 名称                                                     | 描述         |
| ------------------------------------------------------------ | ------------ |
| [ResetAccountPassword](https://intl.cloud.tencent.com/document/product/1042/34430) | 重置帐号密码 |

