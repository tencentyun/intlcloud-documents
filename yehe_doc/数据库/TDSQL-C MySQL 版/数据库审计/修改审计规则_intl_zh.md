本文为您介绍通过控制台修改审计规则相关操作。

## 前提条件
已 [开通审计服务](https://intl.cloud.tencent.com/document/product/1098/44614)。

## 功能说明
- 审计规则支持从全审计变为规则审计，也支持从规则审计变为全审计。
- 审计规则修改后，所选实例将会按照修改后的审计规则进行规则调整。
- 审计规则修改包括规则类型、参数字段、匹配类型、特征串的修改，支持增加和删除规则内容，但需至少保留一条规则内容，修改方法可参见开通审计服务中的 [审计规则设置](https://intl.cloud.tencent.com/document/product/1098/44614)。

## 单实例修改审计规则
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧导航选择**数据库审计**，在上方选择地域。
3. 在审计状态后单击**已开启**过滤出已开启审计服务的实例。
4. 在审计实例列表里找到目标集群/实例（也可在搜索框通过资源属性筛选快速查找），在其**操作**列选择**更多** > **修改审计规则**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/r6AT201_7.png)
5. 在审计规则修改窗口下，完成审计规则的修改，单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nj6N350_8.png)

## 批量修改审计规则
>?
>- 审计规则支持从全审计变为规则审计，也支持从规则审计变为全审计。
>- 批量修改审计规则后，所选实例将会统一按照修改后的审计规则进行审计规则调整。
>- 审计规则修改包括规则类型、参数字段、匹配类型、特征串的修改，支持增加和删除规则内容，但需至少保留一条规则内容，修改方法可参见开通审计服务中的 [审计规则设置]()。

1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧导航选择**数据库审计**，在上方选择地域。
3. 在审计状态后单击**已开启**过滤出已开启审计服务的实例。
4. 在审计实例列表里找到目标集群/实例（也可在搜索框通过资源属性筛选快速查找），在审计实例列表页勾选多个目标实例，单击上方**修改审计规则**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UYwz495_9.png)
5. 在审计规则修改窗口下，完成审计规则的修改，单击**确定**。
>!为方便对比，批量修改审计规则窗口会展示修改前后的审计规则，修改后，所选实例会统一开始按新的审计规则调整，请确认无误后再修改。
>

