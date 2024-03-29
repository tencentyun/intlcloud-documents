## 操作场景

云数据库 MongoDB 审计服务支持根据业务需要长期存储审计日志，满足数据库合规监管要求。 您可以根据业务审计规则的安全合规性要求，随时调整审计日志的保留时长。

## 前提条件

- 已 [创建云数据库 MongoDB 实例](https://intl.cloud.tencent.com/document/product/240/3551)，且实例已开通数据库审计。
- 云数据库 MongoDB 副本集实例或分片实例的状态为**运行中**。

## 操作步骤

1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)。
2. 在左侧导航栏，选择 **MongoDB** > **数据库审计**。
3. 在右侧**数据库审计**页面上方，选择地域。
4. 在审计实例列表的右上角，选择**审计状态**为**已开启**的实例。
5. 单击已开启审计的实例 ID，跳转至**审计日志**页查看对应日志。
6. 在**审计日志**页面右上角，单击**服务设置**。
![](https://qcloudimg.tencent-cloud.cn/raw/e4d6404a7800c33bb1256859d21b772e.png)
7. 在弹出的对话框，修改日志保存时长，单击**提交**。
> ?为满足安全合规性对审计日志保留时长的要求，建议用户选择180天及以上的保存时长。
> 
![](https://qcloudimg.tencent-cloud.cn/raw/66dace29c5ea763aef3bff6b5639524d.png)

