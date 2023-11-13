创建只读实例后，通过购买数据库代理，配置连接地址策略，在应用程序中配置数据库代理地址，就可以使写请求自动转发到主实例，读请求自动转发到各个只读实例。本文介绍通过控制台开启读写分离。

## 前提条件
已 [开通数据库代理](https://intl.cloud.tencent.com/document/product/236/42052)。

## 操作步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在上方选择地域，然后单击目标实例 ID，进入实例管理页。
2. 在实例管理页，选择**数据库代理** > **概览**，在连接地址下找到目标访问地址，在其**操作**列单击**调整配置**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XFJj414_14.png)
3. 在调整配置页面，选择对此访问连接的读写属性，完成读权重分配，单击**确定**。
>?此处的权重是面向读请求（非事务）权重的分配策略。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e4x371_15.png)
