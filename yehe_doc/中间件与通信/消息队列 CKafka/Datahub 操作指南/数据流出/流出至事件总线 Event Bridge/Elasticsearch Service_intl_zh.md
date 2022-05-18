## 操作场景

Datahub 提供数据流出能力，您可以将 CKafka 数据分发至 Elasticsearch Service（ES）便于海量数据存储搜索、实时日志分析等操作。

## 前提条件

该功能目前依赖 SCF、Elasticsearch 服务。使用时需提前开通云函数 SCF、Elasticsearch Service 等相关服务及功能。

## 操作步骤

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据流出**，选择好地域后，单击**新建任务**。
3. 目标类型选择**事件总线（Event Bridge）**，单击**下一步**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/74ec4768fadd95496c41b15fd031ba2b.png)
> ?通过云函数和事件总线处理，需要确认同意 [云函数使用说明](https://intl.cloud.tencent.com/document/product/583) 和 [云函数计费说明](https://intl.cloud.tencent.com/document/product/583/17299)。
4. 在任务设置页面，填写任务详情。
   ![](https://qcloudimg.tencent-cloud.cn/raw/456abbefa1e2efd620c7c4194bca8cdd.png)
   - 任务名称：只能包含字母、数字、下划线、"-"、"."。
   - CKafka 实例：选择数据源 CKafka。
   - 源 Topic：选择源 Topic。
   - 事件目标：选择 **ES**。
   - 起始位置：转储时历史消息的处理方式，topic offset 设置。
   - 自建集群：如 ES 集群为自建集群，请将自建集群开关保持开启状态，并填写示例 IP。如 Elasticsearch 集群为腾讯云集群，则直接选取相关集群信息即可。
   - 实例集群：选取腾讯云 Elasticsearch Service 实例集群信息。
   - 实例用户名：输入 Elasticsearch 实例用户名，腾讯云 Elasticsearch 默认用户名为 elastic，且不可更改。
   - 实例密码：输入 Elasticsearch 实例密码。
   - 云函数授权：知晓并同意开通云函数和事件总线，该函数创建后需用户前往云函数设置更多高级配置及查看监控信息。
4. 单击**提交**，完成任务创建。

### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，单击目标任务的**ID**，进入任务基本信息页面。
3. 在任务详情页顶部，单击**监控**，选择要查看资源，设置好时间范围，可以查看对应的监控数据。



## 产品限制和费用计算

- 转储速度与 CKafka 实例峰值带宽上限有关，如出现消费速度过慢，请检查 CKafka 实例的峰值带宽。
- CKafkaToES 方案采用 CKafka 触发器，重试策略与最大消息数等设置参见 [CKafka 触发器](https://intl.cloud.tencent.com/document/product/583/17530)。
- 使用消息转储 ES 能力，默认转储的信息为 CKafka 触发器的 msgBody 数据，如需自行处理参见 [CKafka 触发器的事件消息结构](https://intl.cloud.tencent.com/document/product/583/17530)。 
- 该功能基于云函数 SCF 服务提供。SCF 为用户提供了一定 [免费额度](https://intl.cloud.tencent.com/document/product/583/12282) ，超额部分产生的收费，请以 SCF 服务的 [计费规则](https://intl.cloud.tencent.com/document/product/583/17299) 为准。
