>! 
> - 本文档中 API 为日志服务旧版本 API，已不再更新，日志服务新增功能均不支持旧版本 API，强烈建议您使用 [日志服务 API 3.0](https://intl.cloud.tencent.com/document/product/614/42757)。
> - 创建日志主题、修改索引配置等管理类操作，请直接使用 [日志服务 API 3.0](https://intl.cloud.tencent.com/document/product/614/42757)。日志采集可使用专为日志采集优化过的 [SDK](https://intl.cloud.tencent.com/document/product/614/45006)。

## API 升级指引
常用旧版本 API 可按下表升级为新版本 API（日志服务 API3.0）:

| 旧：日志服务 API 2017 | API 文档链接                                                  | 新：日志服务API 3.0       | API 文档链接                                                  |
| --------------------- | ------------------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| /topic                | [获取日志主题信息](https://intl.cloud.tencent.com/document/product/614/16887)<br />[修改日志主题](https://intl.cloud.tencent.com/document/product/614/16884) | DescribeTopicsModifyTopic | [获取日志主题列表](https://intl.cloud.tencent.com/document/product/614/42783)<br />[修改日志主题](https://intl.cloud.tencent.com/document/product/614/42782) |
| /searchlog            | [搜索日志](https://intl.cloud.tencent.com/document/product/614/16875) | SearchLog                 | [检索分析日志](https://intl.cloud.tencent.com/document/product/614/42788) |
| /index                | [获取索引信息](https://intl.cloud.tencent.com/document/product/614/16906)<br />[修改索引信息](https://intl.cloud.tencent.com/document/product/614/16905) | DescribeIndexModifyIndex  | [获取索引配置信息](https://intl.cloud.tencent.com/document/product/614/42803)<br />[修改索引](https://intl.cloud.tencent.com/document/product/614/42802) |
| /shipper              | [获取投递配置](https://intl.cloud.tencent.com/document/product/614/16894) | DescribeShipperTasks      | [获取投递任务列表](https://intl.cloud.tencent.com/document/product/614/42773) |
| /pulllogs             | [消费数据](https://intl.cloud.tencent.com/document/product/614/34651) | OpenKafkaConsumer         | [打开Kafka协议消费](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumergroups       | [获取消费组列表](https://intl.cloud.tencent.com/document/product/614/34653) | OpenKafkaConsumer         | [打开Kafka协议消费](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumerheartbeat    | [消费者心跳](https://intl.cloud.tencent.com/document/product/614/34652) | OpenKafkaConsumer         | [打开Kafka协议消费](https://intl.cloud.tencent.com/document/product/614/46784) |
| /cursor               | [获取消费游标](https://intl.cloud.tencent.com/document/product/614/34649) | OpenKafkaConsumer         | [打开Kafka协议消费](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumergroupcursor  | [获取消费组游标](https://intl.cloud.tencent.com/document/product/614/34650)<br />[修改消费组游标](https://intl.cloud.tencent.com/document/product/614/34655) | OpenKafkaConsumer         | [打开Kafka协议消费](https://intl.cloud.tencent.com/document/product/614/46784) |

>?其中/pulllogs、/consumergroups、/consumerheartbeat、/cursor、/consumergroupcursor 接口为日志服务数据消费相关接口，该功能已升级为更加符合开源标准的 Kafka 协议消费功能，您可参照 [Kafka 协议消费](https://intl.cloud.tencent.com/document/product/614/42752) 进行整体升级。



## 日志管理

| 接口名称                                                     | 功能描述                           |
| ------------------------------------------------------------ | ---------------------------------- |
| [上传结构化日志](https://intl.cloud.tencent.com/document/product/614/50267) | 上传日志到指定的日志主题           |
| [获取下载日志游标](https://www.tencentcloud.com/document/product/614/16876) | 获取并下载指定日志主题下的日志游标 |
| [搜索日志](https://intl.cloud.tencent.com/document/product/614/16875) | 根据指定的条件搜索日志内容         |
| [下载日志](https://intl.cloud.tencent.com/document/product/614/16874) | 使用游标下载日志                   |

## 日志集管理

| 接口名称                                                     | 功能描述                    |
| ------------------------------------------------------------ | --------------------------- |
| [创建日志集](https://intl.cloud.tencent.com/document/product/614/16879) | 创建日志集，返回新日志集 ID |
| [获取日志集信息](https://intl.cloud.tencent.com/document/product/614/16881) | 获取日志集信息              |
| [获取日志集列表](https://intl.cloud.tencent.com/document/product/614/16882) | 获取日志集信息列表          |
| [修改日志集](https://intl.cloud.tencent.com/document/product/614/16878) | 修改日志集                  |
| [删除日志集](https://intl.cloud.tencent.com/document/product/614/16880) | 删除日志集                  |

## 日志主题管理

| 接口名称                                                     | 功能描述                        |
| ------------------------------------------------------------ | ------------------------------- |
| [创建日志主题](https://intl.cloud.tencent.com/document/product/614/16885) | 创建日志主题，返回新日志主题 ID |
| [获取日志主题信息](https://intl.cloud.tencent.com/document/product/614/16887) | 获取日志主题信息                |
| [获取日志主题绑定的机器组](https://intl.cloud.tencent.com/document/product/614/30433) | 获取日志主题绑定的机器组信息 |
| [获取日志主题列表](https://intl.cloud.tencent.com/document/product/614/16888) | 获取日志主题信息列表            |
| [修改日志主题](https://intl.cloud.tencent.com/document/product/614/16884) | 修改日志主题                    |
| [设置日志主题绑定的机器组](https://intl.cloud.tencent.com/document/product/614/30434) | 设置日志主题绑定的机器组信息 |
| [删除日志主题](https://intl.cloud.tencent.com/document/product/614/16886) | 删除日志主题                    |
| [获取主题分区列表](https://intl.cloud.tencent.com/document/product/614/34659) |     获取主题分区信息列表              |
| [合并主题分区](https://intl.cloud.tencent.com/document/product/614/34660) |合并一个读写态的主题分区                 |
| [分裂主题分区](https://intl.cloud.tencent.com/document/product/614/34661) | 分裂一个读写态的主题分区                  |




## 投递任务管理

| 接口名称                                                     | 功能描述                   |
| ------------------------------------------------------------ | -------------------------- |
| [创建投递任务](https://intl.cloud.tencent.com/document/product/614/16890) | 创建新的投递任务           |
| [获取投递配置](https://intl.cloud.tencent.com/document/product/614/16894) | 获取指定投递策略的详细信息 |
| [获取日志主题投递列表](https://intl.cloud.tencent.com/document/product/614/30435) | 获取指定日志主题的投递策略详细列表 |
| [获取投递任务列表](https://intl.cloud.tencent.com/document/product/614/16891) | 获取投递任务信息列表       |
| [修改投递任务](https://intl.cloud.tencent.com/document/product/614/16893) | 修改现有的投递任务         |
| [重试失败的任务](https://intl.cloud.tencent.com/document/product/614/16895) | 重试失败的投递任务         |
| [删除投递配置](https://intl.cloud.tencent.com/document/product/614/16892) | 删除投递配置               |

## 机器组管理

| 接口名称                                                     | 功能描述                    |
| ------------------------------------------------------------ | --------------------------- |
| [创建机器组](https://intl.cloud.tencent.com/document/product/614/16899) | 创建机器组，返回新机器组 ID |
| [获取机器组信息](https://intl.cloud.tencent.com/document/product/614/16902) | 获取机器组信息              |
| [获取机器状态](https://intl.cloud.tencent.com/document/product/614/16901) | 获取指定机器组下的机器状态  |
| [获取机器组列表](https://intl.cloud.tencent.com/document/product/614/16903) | 获取机器组信息列表          |
| [修改机器组](https://intl.cloud.tencent.com/document/product/614/16898) | 修改机器组                  |
| [删除机器组](https://intl.cloud.tencent.com/document/product/614/16900) | 删除机器组                  |


## 消费管理

| 接口名称                                                     | 功能描述                    |
| ------------------------------------------------------------ | --------------------------- |
|[创建消费组](https://intl.cloud.tencent.com/document/product/614/34648) | 创建消费组|
| [获取消费游标](https://intl.cloud.tencent.com/document/product/614/34649) | 获取消费游标|
| [获取消费组游标](https://intl.cloud.tencent.com/document/product/614/34650) | 获取消费组游标|
| [消费数据](https://intl.cloud.tencent.com/document/product/614/34651) | 用于消费读取日志|
| [消费者心跳](https://intl.cloud.tencent.com/document/product/614/34652) | 用于消费者上传心跳|
| [获取消费组列表](https://intl.cloud.tencent.com/document/product/614/34653) | 获取日志主题的消费组列表|
| [修改消费组](https://intl.cloud.tencent.com/document/product/614/34654) | 修改消费组|
| [修改消费组游标](https://intl.cloud.tencent.com/document/product/614/34655) | 修改消费组游标信息|
| [删除消费组](https://intl.cloud.tencent.com/document/product/614/34656) | 删除消费组|






## 索引管理

| 接口名称                                                     | 功能描述                   |
| ------------------------------------------------------------ | -------------------------- |
| [获取索引信息](https://intl.cloud.tencent.com/document/product/614/16906) | 获取指定索引策略的详细信息 |
| [修改索引任务](https://intl.cloud.tencent.com/document/product/614/16905) | 修改现有的索引任务         |
