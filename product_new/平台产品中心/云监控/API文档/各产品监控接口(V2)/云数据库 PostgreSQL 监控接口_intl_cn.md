## 1. 接口描述

接口：GetMonitorData
接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询 PostgreSQL 监控数据，入参取值如下：
&Namespace=QCE/POSTGRES
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value 为实例的 resourceId

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1) 文档。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称    | 是否必选 | 类型                                                         | 描述                                                         |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action      | 是       | String                                                       | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String                                                       | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String                                                       | 公共参数，表示查询的是哪个地域实例的监控数据；可查看PostgreSQL支持的 [地域列表](https://intl.cloud.tencent.com/document/product/409/16764) |
| Namespace   | 是       | String                                                       | 命名空间，每个云产品会有一个命名空间，如 PostgreSQL命名空间：QCE/POSTGRES（API 3.0接口版本的必须是大写） |
| MetricName  | 是       | String                                                       | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合                                           |
| Period      | 否       | Integer                                                      | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp                                                    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp                                                    | 结束时间，默认为当前时间。 endTime 不能小于 startTime        |

#### 2.1.2 各维度对应参数总览

| 参数名称                       | 维度名称   | 维度解释             | 格式                                          |
| :----------------------------- | :--------- | :------------------- | :-------------------------------------------- |
| Instances.N.Dimensions.0.Name  | resourceId | 实例的resourceId     | 输入String类型维度名称，如：resourceId        |
| Instances.N.Dimensions.0.Value | resourceId | 实例具体的resourceId | 输入实例的具体resourceId，如：postgres-123456 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称       | 含义               | 单位    |
| :------------- | :----------------- | :------ |
| Connections    | 连接数             | 个      |
| Cpu            | CPU 利用率         | %       |
| HitPercent     | 缓冲区缓存命中率   | %       |
| InFlow         | 输入流量           | KB/秒   |
| OutFlow        | 输出流量           | KB/秒   |
| Iops           | 磁盘 IOPS          | 次/秒   |
| Memory         | 内存占用           | KB      |
| OtherCalls     | 其他请求数         | 次/分钟 |
| Qps            | 每秒查询数         | 次/秒   |
| WriteCalls     | 写请求数           | 次/分钟 |
| ReadCalls      | 读请求数           | 次/分钟 |
| ReadWriteCalls | 读写请求数         | 次/分钟 |
| RemainXid      | 剩余XID数量        | 个      |
| SqlRuntimeAvg  | 平均执行时延       | Ms      |
| SqlRuntimeMax  | 最长TOP10执行时延  | Ms      |
| SqlRuntimeMin  | 最短TOP10执行时延  | Ms      |
| Storage        | 已用存储空间       | GB      |
| XlogDiff       | 主备 XLOG 同步差异 | Byte    |

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
| -513     | DB 操作失败    | InternalError.DBoperationFail        |

## 5. 示例

### 示例1

拉取某个 PostgreSQL 某段时间内统计周期为60秒的连接数监控数据。

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/POSTGRES
&MetricName=Connections
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=postgres-123456
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-123456"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      }
    ],
    "RequestId": "d2141cc8-74e2-4e55-905e-3780d7d654df"
  }
}
```

### 示例2

拉取多个 PostgreSQL 某段时间内统计周期为60秒的连接数监控数据。

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/BLOCK_STORAGE
&MetricName=Connections
&Period=60
&StartTime=2019-05-28T10:40:00+08:00
&EndTime=2019-05-28T10:45:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=postgres-123456
&Instances.1.Dimensions.0.Name=resourceId
&Instances.1.Dimensions.0.Value=postgres-654321
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-05-28 10:40:00",
    "EndTime": "2019-05-28 10:45:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-123456"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-654321"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      }
    ],
    "RequestId": "d2141cc8-74e2-4e55-905e-3780d7d654df"
  }
}
```