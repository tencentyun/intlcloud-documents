## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询消息队列分组消费监控数据，入参取值如下：

&Namespace=QCE/CKAFKA

&Instances.N.Dimensions.0.Name=consumerGroup

&Instances.N.Dimensions.0.Value=消费分组

&Instances.N.Dimensions.1.Name=instanceId

&Instances.N.Dimensions.1.Value=实例 ID

&Instances.N.Dimensions.2.Name=topicId

&Instances.N.Dimensions.2.Value=主题 ID

&Instances.N.Dimensions.3.Name=topicName

&Instances.N.Dimensions.3.Value=主题名称

&Instances.N.Dimensions.4.Name=partition

&Instances.N.Dimensions.4.Value=分区




## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共请求参数，正式调用时需要加上公共请求参数，详情请参见[公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/CKAFKA |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------------------ | ------------- | ------------- | ------------------------------------------------ |
| Instances.N.Dimensions.0.Name | consumerGroup | consumerGroup | String 类型维度名称：consumerGroup |
| Instances.N.Dimensions.0.Value | consumerGroup | 消费分组信息 | 用户需要查看的消费分组信息，如 perf-consumer-8330 |
| Instances.N.Dimensions.1.Name | instanceId | instanceId | String 类型维度名称：instanceId |
| Instances.N.Dimensions.1.Value | instanceId | 实例 ID | 用户需要查看监控的实例 ID，如 ckafka-test |
| Instances.N.Dimensions.2.Name | topicId | topicId | String 类型维度名称：topicId |
| Instances.N.Dimensions.2.Value | topicId | 主题 ID | 用户订阅主题 ID，如 topic-test |
| Instances.N.Dimensions.3.Name | partition | partition | String 类型维度名称：partition |
| Instances.N.Dimensions.3.Value | partition | partition 信息 | topic 分区信息，如0 |
| Instances.N.Dimensions.4.Name | topicName | topicName | String 类型维度名称：topicName |
| Instances.N.Dimensions.5.Value | topicName | 主题名称| 用户消费主题的名称，如test |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称 | 含义 | 单位 | 维度 |
| ------------------------ | ------------------------------------------- | ---- | ----------------------------------------------------- |
| CgroupMaxOffset | 消费分组对应 partition 的最大 offset | 条 | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicMsgOffset | 消费分组对应 partition 当前消费 offset | 条 | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicUnconsumeMsgCount | 消费分组对应 partition 未被消费消息条数 | 条 | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicUnconsumeMsgOffset | 消费分组对应 partition 未被消费的消息总大小 | MB | consumerGroup,instanceId,topicId, partition,topicName |



## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId |

## 4. 示例

### 示例1 

拉取某个消息队列分组消费某段时间内统计周期为60秒的消费分组对应 partition 未被消费的消息总大小监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicUnconsumeMsgOffset
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=consumerGroup
&Instances.0.Dimensions.0.Value=perf-consumer-8330
&Instances.0.Dimensions.1.Name=instanceId
&Instances.0.Dimensions.1.Value=ckafka-test
&Instances.0.Dimensions.2.Name=topicId
&Instances.0.Dimensions.2.Value=topic-test
&Instances.0.Dimensions.3.Name=topicName
&Instances.0.Dimensions.3.Value=test
&Instances.0.Dimensions.4.Name=partition
&Instances.0.Dimensions.4.Value=0
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-21 20:35:00",
"EndTime": "2019-05-21 20:40:00",
"Period": 60,
"MetricName": "CtopicUnconsumeMsgOffset",
"DataPoints": [
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-8330"
},
{
"Name": "instanceId",
"Value": "ckafka-test"
},
{
"Name": "partition",
"Value": "0"
},
{
"Name": "topicId",
"Value": "topic-test"
},
{
"Name": "topicName",
"Value": "test"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
}
],
"RequestId": "c57cb169-606e-4617-a063-12345678910"
}
}
```

### 示例2 

拉取多个消息队列分组消费某段时间内统计周期为60秒的消费分组对应 partition 未被消费的消息总大小监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicUnconsumeMsgOffset
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=consumerGroup
&Instances.0.Dimensions.0.Value=perf-consumer-83301
&Instances.0.Dimensions.1.Name=instanceId
&Instances.0.Dimensions.1.Value=ckafka-test1
&Instances.0.Dimensions.2.Name=topicId
&Instances.0.Dimensions.2.Value=topic-test1
&Instances.0.Dimensions.3.Name=topicName
&Instances.0.Dimensions.3.Value=test1
&Instances.0.Dimensions.4.Name=partition
&Instances.0.Dimensions.4.Value=0
&Instances.1.Dimensions.0.Name=consumerGroup
&Instances.1.Dimensions.0.Value=perf-consumer-83302
&Instances.1.Dimensions.1.Name=instanceId
&Instances.1.Dimensions.1.Value=ckafka-test2
&Instances.1.Dimensions.2.Name=topicId
&Instances.1.Dimensions.2.Value=topic-test2
&Instances.1.Dimensions.3.Name=topicName
&Instances.1.Dimensions.3.Value=test2
&Instances.1.Dimensions.4.Name=partition
&Instances.1.Dimensions.4.Value=1
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-21 20:35:00",
"EndTime": "2019-05-21 20:40:00",
"Period": 60,
"MetricName": "CtopicUnconsumeMsgOffset",
"DataPoints": [
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-83301"
},
{
"Name": "instanceId",
"Value": "ckafka-test1"
},
{
"Name": "partition",
"Value": "1"
},
{
"Name": "topicId",
"Value": "topic-test1"
},
{
"Name": "topicName",
"Value": "test1"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
},
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-83302"
},
{
"Name": "instanceId",
"Value": "ckafka-test2"
},
{
"Name": "partition",
"Value": "2"
},
{
"Name": "topicId",
"Value": "topic-test2"
},
{
"Name": "topicName",
"Value": "test2"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
}
],
"RequestId": "c57cb169-606e-4617-a063-12345678910"
}
}
```