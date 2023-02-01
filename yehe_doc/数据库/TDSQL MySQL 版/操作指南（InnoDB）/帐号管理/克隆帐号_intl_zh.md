## 操作场景
您可以通过 TDSQL MySQL版 控制台可以对数据库帐号进行克隆，保留原帐号密码，并在不同主机上提供不同权限。

## 操作步骤
1. 登录 [TDSQL 控制台](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)，在**实例列表**中，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**帐号管理**页，找到需要重置密码的帐号，单击**克隆帐号**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZcNv667_3.png)
3. 在弹出的对话框，填写主机 IP，帐号密码均复制原帐号形式，单击**确认，下一步**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xHeX802_4.png)
4. 返回帐号管理页，即可看到克隆的帐号。

## 相关 API

| API 名称                                                     | 描述         |
| ------------------------------------------------------------ | ------------ |
| [CloneAccount](https://intl.cloud.tencent.com/document/product/1042/34452) | 克隆实例帐号 |

