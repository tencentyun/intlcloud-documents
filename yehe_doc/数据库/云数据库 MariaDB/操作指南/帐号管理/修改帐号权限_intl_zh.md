## 操作场景
通过云数据库 MariaDB 控制台可以对数据库帐号授予操作权限，可授予全局特权和对象级特权。

## 操作步骤
1. 登录 [MariaDB 控制台](https://console.cloud.tencent.com/mariadb)，在**实例列表**中，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**帐号管理**页，找到需要修改权限的帐号，单击**修改权限**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/L9Sg182_1.png)
3. 在弹出的对话框，选中或者取消需要授予的权限，单击**确定**。
 - 全局特权：拥有实例下所有数据库的所有权限。
 - 对象级特权：拥有实例下特定数据库的权限。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9DZI240_2.png)

## 相关 API

| API 名称                                                     | 描述         |
| ------------------------------------------------------------ | ------------ |
| [DescribeAccountPrivileges](https://intl.cloud.tencent.com/document/product/237/16164) | 查询帐号权限 |
| [GrantAccountPrivileges](https://intl.cloud.tencent.com/document/product/237/16166) | 设置帐号权限 |

