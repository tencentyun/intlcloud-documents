本文为您介绍账号管理列表相关字段和信息。

## 数据库账号
当您创建 SQL Server 实例后，可以创建不同的数据库账号，根据业务需要用不同的账号分配管理数据库。

## 查看账号管理列表
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)。
2. 在实例列表找到目标实例，单击其**操作**列的**管理**进入实例详情页。
3. 单击**账号管理**即可进入账号管理页。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/a6Aj811_11.png)

## 工具项
| 工具 | 说明 |
|---------|---------|
| 搜索框 | 单击![](https://qcloudimg.tencent-cloud.cn/raw/4e9962a6b05796851af7e63f3bea18dc.png)进行过滤，支持模糊搜索账号名快速查找相关账号。 |
| 刷新 | 单击![](https://qcloudimg.tencent-cloud.cn/raw/309481e9077b12e66da812127caa683a.png)可刷新列表。 |

## 账号列表字段信息

| 字段 | 说明 |
|---------|---------|
| 账号名 | 显示实例下已创建的所有账号名称。 |
| 账号类型 | 显示实例下已创建账号的类型，不同实例架构支持创建的账号类型如下：<br>**双节点**<li>高级权限账号：实例管理员账号，默认对所有数据库有所有者权限。<li>普通账号：非管理员账号，支持指定对某数据库的读写、只读、所有者权限。<li>特殊权限账号：此特殊账号仅能看到指定数据库且拥有指定数据库的所有者权限。一个特殊权限账号可以授权给多个数据库，但是一个数据库仅能被授权给一个特殊权限账号。<br>**单节点**<li>超级权限账号：实例管理员账号，具备最高管理 sysadmin 权限，并对所有数据库有所有者权限，<strong>启用超级权限账号，产品将不再保障实例 SLA</strong>。<li>高级权限账号：实例管理员账号，默认对所有数据库有所有者权限。<li>普通账号：非管理员账号，支持指定对某数据库的读写、只读、所有者权限。<li>特殊权限账号：此特殊账号仅能看到指定数据库且拥有指定数据库的所有者权限。一个特殊权限账号可以授权给多个数据库，但是一个数据库仅能被授权给一个特殊权限账号。 |
| 状态 | 显示对应账号的状态。 |
| 账号创建时间 | 显示创建账号的时间，支持升序和降序排列。 |
| 账号更新时间 | 显示更新账号相关信息的时间，支持升序和降序排列。 |
| 密码最新更新时间 | 显示最新重置账号密码的时间，支持升序和降序排列。 |
| 所属数据库 | 显示对应账号所被授权访问的数据库。 |
| 备注 | 显示对应账号的备注描述。 |
| 操作 | <li>设置权限：为账号设置对指定数据库的读写或只读权限。<li>重置密码：为账号重置密码。<li>删除账号：删除对应账号。 |

>?账号列表的各个操作功能，均支持勾选多个账号后，通过单击账号列表上方的**批量管理**对应批量操作。
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/HciT537_15.png)

## 相关操作
- [创建账号](https://intl.cloud.tencent.com/document/product/238/7521)
- [修改账号权限](https://intl.cloud.tencent.com/document/product/238/35795)
- [重置密码](https://intl.cloud.tencent.com/document/product/238/35796)
- [删除账号](https://intl.cloud.tencent.com/document/product/238/35794)

  
