### 如何授权某个主机地址的客户端对云数据库 MySQL 的访问？
您可以通过 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 修改数据库帐号所授权的主机地址，来管控对数据库的访问。 
  
### 为什么无法登录数据库管理工具 DMC？
1）可能是您使用的业务帐号导致的，需要前往 [数据库账号管理](https://console.cloud.tencent.com/cdb)，确认登录账号已对要访问数据库的主机地址客户端授权，将主机地址设置为“%”或者您要授权访问的客户端主机地址。
![](https://main.qcloudimg.com/raw/2e0f60d3237e8e244b51dd7e164de315.png)  

您也可以使用 root 帐号直接登录数据库管理工具。

2）若确认不是以上问题，则可能是您的帐号密码错误，请重新输入您的密码，或者 [重置密码](https://intl.cloud.tencent.com/document/product/236/31901)。


### 为什么无法创建数据库/表？
有可能是您登录的帐号为业务帐号，没有创建数据库/表的权限，请您在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 对该帐号赋予权限，如下图所示。  
![](https://main.qcloudimg.com/raw/b33188cf3aba103b415c0ecc38fb0168.png)

### 为什么没有权限修改数据库参数，如 sql_mode？
可能是用户使用的子账号没有修改实例参数的权限，需要用主账号来操作，或者进行 [访问管理 CAM](https://intl.cloud.tencent.com/document/product/236/14469) 来授权子账号的相关操作权限。

### 如何设置子账号修改 MySQL 权限？
如果您想让用户拥有创建和管理云数据库实例的权限，您可以对该用户使用名称为：QcloudCDBFullAccess 的策略  ，详情请参见 [云数据库的全读写策略](https://intl.cloud.tencent.com/document/product/236/14468)。


