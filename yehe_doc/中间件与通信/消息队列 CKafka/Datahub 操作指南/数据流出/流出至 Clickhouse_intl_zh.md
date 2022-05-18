## 操作场景

DataHub 提供数据流出能力，您可以将 CKafka 数据分发至数据仓库 ClickHouse 以对数据进行存储、查询和分析。

## 前提条件

- 若使用腾讯云维护的 ClickHouse 产品，使用时需开通相关产品功能。同时也支持数据流出至自建 ClickHouse。
- 在 ClickHouse 建好表，建表的时候需要指定好 Column 和 Type。

## 操作步骤

### 创建任务

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，选择好地域后，单击**新建任务**。
3. 目标类型选择**数据仓库 ClickHouse**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/491af4f90cf7371429b5feeeb92fe17e.png)

### 配置 CKafka 数据源
在页面中设置 CKafka 数据源相关设置，相关配置如下：
1. **任务名称**：只能包含字母、数字、下划线、"-"、"."。
2. **CKafka 实例**：选择数据源 CKafka。
3. **源 Topic**：选择实例下的 Topic，一条数据流出任务最多支持选择 5 个源 Topic，选中的 Topic 内的数据格式需要保持一致方可转储成功。

### 消息解析
上述设置后，单击**预览数据**，将会选取**源 Topic** 中的第一条消息进行解析。
>? 目前解析消息需要满足以下条件：
>- 消息为 JSON 字符串结构。
>- 解析后的消息为单层 JSON，即目前无法解析嵌套结构的 JSON。
> 
> 当消息不为单层 JSON 结构时，推荐使用 [**数据处理**](https://console.intl.cloud.tencent.com/ckafka/datahub-process) 进行简单的消息格式转换。 
> 
单击解析后，控制台将会出现解析后的消息字段，可以通过修改预览结果中的 type 属性来确定投递到目标对应列的类型。
当选择 type 为 `Date` 或 `DateTime` 时，如果源消息格式为整型，将会尝试使用 `unix timestamp` 格式解析；如果源消息格式为字符串，将会尝试用常用的时间格式模式串解析。

### 流出配置
根据流出目标 ClickHouse 不同，分为了 [**云数据仓库 ClickHouse**](https://console.intl.cloud.tencent.com/cdwch) 和 **自建 ClickHouse** 两类。
<dx-tabs>
::: 云数据仓库 ClickHouse [](id:UseCDWClickHouseSink)
由于 **云数据仓库 ClickHouse** 在创建的时候就已经使用私有连接进行封装，因此可以直接在控制台选择对应的 **云数据仓库 ClickHouse** 实例，数据流出会自动进行相关 vpc 网络的打通。
:::

::: 自建或 emr ClickHouse [](id:UseSelfHostOrEMRClickHouseSink)
由于 CKafka 实例采用的是托管实例的形式，而 emr ClickHouse 是直接在购买的 CVM 上创建公网路由，因此需要用户手动在此基础上创建负载均衡服务，才能打通 VPC 服务。下面以 emr ClickHouse 为例创建负载均衡：
打开 [emr 控制台](https://console.intl.cloud.tencent.com/emr) ，选取目标集群，依次单击 **集群资源**，**节点状态**，在状态页中找到 ClickHouse 的节点 IP。
进入 [负载均衡](https://console.intl.cloud.tencent.com/clb) 控制台，新建一个负载均衡实例后，单击上方导航栏的 **监听器管理**，在页面中单击新建 **TCP/UDP/TCP SSL 监听器**，在端口中填写**数据流出时用到的端口**。
创建监听器后，单击 **绑定后台服务**，输入 ClickHouse 中的 tcp 端口，默认应为 9000。
绑定完成后，即可在数据流出控制台选择当前创建的负载均衡服务，端口填写的是 **负载均衡** 服务中监听的端口。

>? 目前仅支持创建与负载均衡同一地域的数据流出 ClickHouse 服务。
>
:::
</dx-tabs>

网络打通后，还需要配置数据流出实例其余选项，说明如下：
- 用户名：目标 ClickHouse 的用户名（默认为 `default`）。
- 密码：目标 ClickHouse 的密码。
>!出于安全考虑，数据流出 ClickHouse 中密码为必填项。
> 目前实例创建后可能密码为空，此时需要在配置文件 `user.xml` 中修改密码。具体可参考 [ClickHouse 官方文档](https://clickhouse.com/docs/en/operations/settings/settings-users/) 。 
- cluster： ClickHouse 的集群名称（默认为 `default_cluster`）。
- database：ClickHouse 设置的数据库名称。
- table：在该数据库内构建的表名称，目前数据流出 ClickHouse 服务不会自动创建表，**需要客户手动创建当前 ClickHouse 目标表**。
- 丢弃解析消息：消息解析失败原因一般是消息字段与目标库字段 type 不一致。若不丢弃解析失败消息，则任务异常，转储不再继续。

最后单击**提交**，即可完成任务创建。

## 监控配置


1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流出**，单击目标任务的 **ID**，进入任务基本信息页面。
3. 在任务详情页顶部，单击**监控**，选择要查看资源，设置好时间范围，可以查看对应的监控数据。


## 产品限制和费用计算

转储速度与 CKafka 实例峰值带宽上限有关，如出现消费速度过慢，请检查 CKafka 实例的峰值带宽或增加 CKafka partition 数。
