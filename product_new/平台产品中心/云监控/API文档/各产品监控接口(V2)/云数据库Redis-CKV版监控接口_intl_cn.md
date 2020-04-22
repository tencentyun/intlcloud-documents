## 1. 接口描述

接口：GetMonitorData
接口请求域名： `monitor.tencentcloudapi.com`

本接口支持获取 **Redis 2.8集群版，CKV标准版，CKV集群版** 3个版本的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。 若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库Redis监控数据，入参取值如下：
&Namespace= QCE/REDIS
&Instances.N.Dimensions.0.Name=redis_uuid
&Instances.N.Dimensions.0.Value 为实例的 uuid

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1) 文档。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称    | 是否必选 | 类型                                                         | 描述                                                         |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action      | 是       | String                                                       | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String                                                       | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String                                                       | 公共参数，表示查询的是哪个地域实例的监控数据；可查看云数据库Redis支持的 [地域列表](https://intl.cloud.tencent.com/document/product/239/32045) |
| Namespace   | 是       | String                                                       | 命名空间，每个云产品会有一个命名空间，如云数据库Redis命名空间： QCE/REDIS（API 3.0接口版本的必须是大写） |
| MetricName  | 是       | String                                                       | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合                                           |
| Period      | 否       | Integer                                                      | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp                                                    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp                                                    | 结束时间，默认为当前时间。 endTime 不能小于 startTime        |

#### 2.1.2 各维度对应参数总览

| 参数名称                       | 维度名称   | 维度解释     | 格式                                   |
| :----------------------------- | :--------- | :----------- | :------------------------------------- |
| Instances.N.Dimensions.0.Name  | redis_uuid | 实例的 ID    | 输入String类型维度名称，如：redis_uuid |
| Instances.N.Dimensions.0.Value | redis_uuid | 具体实例的id | 输入具体实例 ID，如：crs-123456        |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标中文名 | 指标英文名  | 指标采集方式（Linux下含义）                                  | 指标统计方式                                     | 单位    |
| :--------- | :---------- | :----------------------------------------------------------- | :----------------------------------------------- | :------ |
| 总请求     | Qps         | 1分钟内命令总数除以60                                        | 每分钟采集，5分钟粒度数据是按最近5分钟内求平均值 | 次/秒钟 |
| 连接数量   | Connections | 1分钟内连接数总和                                            | 每分钟采集，5分钟粒度数据是按最近5分钟内求和     | 个      |
| CPU使用率  | CpuUs       | CPU处于非空闲状态的百分比，取 /proc/stat数据计算得出         | 每分钟采集，5分钟粒度数据是按最近5分钟内求平均值 | %       |
| 入流量     | InFlow      | 1分钟内入流量总和                                            | 每分钟采集，5分钟粒度数据是按最近5分钟内求和     | Mb/分钟 |
| Key总个数  | Keys        | 1分钟内key数量的最大值                                       | 每分钟采集，5分钟粒度数据是按最近5分钟内求最大值 | 个      |
| 出流量     | OutFlow     | 1分钟内出流量总和                                            | 每分钟采集，5分钟粒度数据是按最近5分钟内求和     | Mb/分钟 |
| 写请求     | StatGet     | 1分钟内 get, hget, hgetall, hmget, mget, getbit, getrange 命令请求数 | 每分钟采集，5分钟粒度数据是按最近5分钟内求和     | 次/分钟 |
| 读请求     | StatSet     | 1分钟内 set, hset, hmset, hsetnx, lset, mset, msetnx, setbit, setex, setrange, setnx 命令请求数 | 每分钟采集，5分钟粒度数据是按最近5分钟内求和     | 次/分钟 |
| 内存使用量 | Storage     | 1分钟内已使用容量的最大值                                    | 每分钟采集，5分钟粒度数据是按最近5分钟内求最大值 | MB/分钟 |
| 内存使用率 | StorageUs   | 1分钟内已使用容量的百分比最大值                              | 每分钟采集，5分钟粒度数据是按最近5分钟内求最大值 | %       |

## 3. 输出参数

| 参数名称   | 类型                  | 描述                                                         |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String                | 监控指标                                                     |
| StartTime  | Timestamp             | 数据点起始时间                                               |
| EndTime    | Timestamp             | 数据点结束时间                                               |
| Period     | Integer               | 数据统计周期                                                 |
| DataPoints | Array of PointsObject | 监控数据列表                                                 |
| RequestId  | String                | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId |

## 4. 错误码表

| 错误代码 | 错误描述       | 英文描述                             |
| :------- | :------------- | :----------------------------------- |
| -502     | 资源不存在     | OperationDenied.SourceNotExists      |
| -503     | 请求参数有误   | InvalidParameter                     |
| -505     | 参数缺失       | InvalidParameter.MissingParameter    |
| -507     | 超出限制       | OperationDenied.ExceedLimit          |
| -509     | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513     | DB操作失败     | InternalError.DBoperationFail        |

## 5. 在线调试

您可以通过 [在线调试工具](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=) 进行API调试。

## 6. 示例

### 示例1

拉取某个云数据库 Redis 某段时间内统计周期为60秒的连接数监控数据。

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:00:00",
    "EndTime": "2019-06-04 00:05:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-123456"
          }
        ],
        "Timestamps": [
          1557304800,
          1557304860,
          1557304920,
          1557304980,
          1557305040,
          1557305100
        ],
        "Values": [
          3,
          3,
          4.5,
          3,
          3
        ]
      }
    ],
    "RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
  }
}
```

### 示例2

拉取某个云数据库 Redis 某段时间内统计周期为60秒的连接数监控数据。

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=redis_uuid
&Instances.1.Dimensions.0.Value=crs-1234567
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:00:00",
    "EndTime": "2019-06-04 00:05:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-123456"
          }
        ],
        "Timestamps": [
          1557304800,
          1557304860,
          1557304920,
          1557304980,
          1557305040,
          1557305100
        ],
        "Values": [
          3,
          3,
          4.5,
          3,
          3
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-1234567"
          }
        ],
        "Timestamps": [
          1557304800,
          1557304860,
          1557304920,
          1557304980,
          1557305040,
          1557305100
        ],
        "Values": [
          3,
          3,
          4.5,
          3,
          3
        ]
      }
    ],
    "RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
  }
}
```