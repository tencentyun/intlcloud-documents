##  配置集群日志服务
### 集群日志配置说明
ClickHouse 支持将节点日志采集至您帐号下的日志服务（CLS），您可按需操作是否开启和使用日志检索功能。
>?CLS 服务为后付费形式请确认费用充足，以免影响您的 ClickHouse 日志上传和展示。CLS 日志费用说明详见 [计费概述](https://intl.cloud.tencent.com/document/product/614/37509)。开启日志服务，授权日志服务权限将同步生效。

### 开启集群日志功能
- 新建集群开启日志服务 
支持集群创建时配置日志服务，开启日志配置选项，选择集群同地域的日志服务（CLS）的日志集（可跳转新建日志集），默认日志保存时间为30天。
![](https://qcloudimg.tencent-cloud.cn/raw/521f9e0caecbaf9f98eba7594f3409f4.png)
>?我们会在您配置的日志集中创建新的日志主题，用于存储 ClickHouse 相关日志。您可以通过 CLS 日志服务页面查看您的日志主题，已配置到 ClickHouse 集群的日志主题切记勿删除，若配置的日志主题被删除将会导致 ClickHouse 日志检索页查询失败。
>
- 已有集群开启或修改日志服务
ClickHouse 集群创建未开启日志服务时，用户可以随时通过集群列表的**操作 > 更多 > 新建日志服务**配置日志服务。对于未授权用户，需要授权后，再配置日志集。
 ![](https://qcloudimg.tencent-cloud.cn/raw/3727abbf1528b8a69c3d7a6aac472a33.png)

## 使用日志检索
1. 登录 [云数据仓库 ClickHouse 控制台](https://console.cloud.tencent.com/cdwch)，在**集群列表**中单击**集群 ID/名称**进入集群详情页，切换到**日志检索**页签。
2. 支持选择节点日志和搜索两种页面模式，支持运行日志和错误日志筛选，根据条件查看对应各个节点的日志。
 ![](https://qcloudimg.tencent-cloud.cn/raw/7ed0845d6e901cd98bf17465d4744d6c.png)
3. 支持查询包含关键字的日志记录，筛选结果按照节点 IP 进行分组，以便查看各个节点的搜索结果。查询结果默认展示各个节点最近100条记录。
![](https://qcloudimg.tencent-cloud.cn/raw/b23f4d81b49bbed77b0bcb7d98a567b7.png)
