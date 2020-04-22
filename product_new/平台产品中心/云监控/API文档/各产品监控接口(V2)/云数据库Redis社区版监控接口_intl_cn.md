## 1. 接口描述

接口：GetMonitorData
接口请求域名： monitor.tencentcloudapi.com

本接口支持获取 **Redis 2.8、4.0、5.0标准版和集群版** 的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。 若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库REDIS监控数据，入参取值如下：
&Namespace=QCE/REDIS
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value为实例的id

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，见 [公共请求参数](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1) 页面。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称    | 是否必选 | 类型                                                         | 描述                                                         |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action      | 是       | String                                                       | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String                                                       | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String                                                       | 公共参数，表示查询的是哪个地域实例的监控数据；可查看云数据库REDIS支持的 [地域列表](https://intl.cloud.tencent.com/document/product/239/32045) |
| Namespace   | 是       | String                                                       | 命名空间，每个云产品会有一个命名空间，如云数据库REDIS命名空间： QCE/REDIS（API 3.0接口版本的必须是大写） |
| MetricName  | 是       | String                                                       | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合                                           |
| Period      | 否       | Integer                                                      | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp                                                    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp                                                    | 结束时间，默认为当前时间。 endTime不能小于startTime          |

#### 2.1.2 各维度对应参数总览

| 参数名称                       | 维度名称   | 维度解释     | 格式                                                         |
| :----------------------------- | :--------- | :----------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | instanceid | 实例的id     | 输入String类型维度名称，如：instanceid                       |
| Instances.N.Dimensions.0.Value | instanceid | 具体实例的id | 输入实例的具体redis实例id，如：tdsql-123456 也即是实例串号，如：crs-ifmymj41，可通过 [查询CRS实例列表接口](https://intl.cloud.tencent.com/document/product/239/1384) 查询 |
| Instances.N.Dimensions.1.Name  | clusterid  | 分片的id     | 输入String类型维度名称，如：clusterid 。如拉取总信息，不传此值；如拉取分片信息，入参必现是clusterid |
| Instances.N.Dimensions.1.Value | clusterid  | 具体分片的id | 输入具体分片id，如：tdsql-123456 ，可通过命令cluster nodes等获取分片id |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

#### 2.2.1 标准版监控指标信息

| 指标名称         | 指标含义         | 单位  | 指标说明                                                     |
| :--------------- | :--------------- | :---- | :----------------------------------------------------------- |
| CpuUsMin         | CPU使用率        | %     | 平均CPU使用率                                                |
| StorageMin       | 内存使用量       | %     | 实际使用内存容量，包含数据和缓存部分                         |
| StorageUsMin     | 内容使用率       | MB    | 实际使用内存和申请总内存之比                                 |
| KeysMin          | Key总数          | 个    | 实例存储的总Key个数（一级Key）                               |
| ExpiredKeysMin   | key过期数        | 个    | 时间窗内被淘汰的Key个数，对应info命令输出的expired_keys      |
| EvictedKeysMin   | key驱逐数        | 个    | 时间窗内被驱逐的Key个数，对应info命令输出的evicted_keys      |
| ConnectionsMin   | 连接数量         | 个    | 连接到实例的TCP连接数量                                      |
| ConnectionsUsMin | 连接数使用率     | %     | 实际TCP连接数量和最大连接数比                                |
| InFlowMin        | 入流量           | Mb/S  | 内网入流量                                                   |
| InFlowUsMin      | 入流量使用率     | %     | 内网入流量实际使用和最大流量比                               |
| OutFlowMin       | 出流量           | Mb/S  | 内网出流量                                                   |
| OutFlowUsMin     | 出流量使用率     | %     | 内网出流量实际使用和最大流量比                               |
| LatencyMin       | 平均执行时延     | ms    | proxy到redis server的执行时延平均值                          |
| LatencyGetMin    | 读平均时延       | ms    | proxy到redis server的读命令平均执行时延，读命令分类，请查看文档监控说明 |
| LatencySetMin    | 写平均时延       | ms    | proxy到redis server的写命令平均执行时延，读命令分类，请查看文档监控说明 |
| LatencyOtherMin  | 其他命令平均时延 | ms    | proxy到redis server的读写命令之外的命令平均执行时延，其他命令分类，请查看文档监控说明 |
| QpsMin           | 总请求           | 次/秒 | QPS，命令执行次数                                            |
| StatGetMin       | 读请求           | 次/分 | 读命令执行次数，读命令分类，请查看文档监控说明               |
| StatSetMin       | 写请求           | 次/分 | 写命令执行次数，读命令分类，请查看文档监控说明               |
| StatOtherMin     | 其他请求         | 次/秒 | 读写命令之外的命令执行次数，其他命令分类，请查看文档监控说明 |
| BigValueMin      | 大Value请求      | 次/秒 | 请求命令大小超过32KB的执行次数                               |
| SlowQueryMin     | 慢查询           | 次    | 慢查询命令次数                                               |
| StatSuccessMin   | 读请求命中       | 次    | 读请求Key存在的个数，对应info命令输出的keyspace_hits指标     |
| StatMissedMin    | 读请求Miss       | 次    | 读请求Key不存在的个数，对应info命令输出的keyspace_misses指标 |
| CmdErrMin        | 执行错误         | 次    | 命令执行错误的次数，例如命令不存在、参数错误等情况           |
| CacheHitRatioMin | 读请求命中率     | %     | Key命中/(Key命中+KeyMiss)，该指标可以反应Cache Miss的情况    |

#### 2.2.2 集群版汇总指标信息

| 指标名称         | 指标含义           | 单位  | 指标说明                                                     |
| :--------------- | :----------------- | :---- | :----------------------------------------------------------- |
| CpuUsMin         | 平均CPU使用率      | %     | 平均CPU使用率                                                |
| CpuMaxUs         | 分片最大CPU使用率  | %     | 集群所有分片中，CPU使用率最高值                              |
| StorageMin       | 内存使用量         | %     | 实际使用内存容量，包含数据和缓存部分                         |
| StorageUsMin     | 内存使用率         | MB    | 实际使用内存和申请总内存之比                                 |
| StorageMaxUs     | 分片最大内存使用率 |       | 集群所有分片中，内存使用率最高值                             |
| KeysMin          | Key总个数          | 个    | 实例存储的总Key个数（一级Key）                               |
| ExpiredKeysMin   | key过期数          | 个    | 时间窗内被淘汰的Key个数，对应info命令输出的expired_keys      |
| EvictedKeysMin   | key驱逐数          | 个    | 时间窗内被驱逐的Key个数，对应info命令输出的evicted_keys      |
| ConnectionsMin   | 连接数量           | 个    | 连接到实例的TCP连接数量                                      |
| ConnectionsUsMin | 连接数使用率       | %     | 实际TCP连接数量和最大连接数比                                |
| InFlowMin        | 入流量             | Mb/S  | 内网入流量                                                   |
| InFlowUs         | 入流量使用率       | %     | 内网入流量实际使用和最大流量比                               |
| OutFlowMin       | 出流量             | Mb/S  | 内网出流量                                                   |
| OutFlowUs        | 出流量使用率       | %     | 内网出流量实际使用和最大流量比                               |
| LatencyMin       | 平均执行时延       | ms    | proxy到redis server的执行时延平均值                          |
| LatencyGetMin    | 读平均时延         | ms    | proxy到redis server的读命令平均执行时延，读命令分类，请查看文档监控说明 |
| LatencySetMin    | 写平均时延         | ms    | proxy到redis server的写命令平均执行时延，读命令分类，请查看文档监控说明 |
| LatencyOtherMin  | 其他命令平均时延   | ms    | proxy到redis server的读写命令之外的命令平均执行时延，其他命令分类，请查看文档监控说明 |
| QpsMin           | 总请求             | 次/秒 | QPS，命令执行次数                                            |
| StatGetMin       | 读请求             | 次/秒 | 读命令执行次数，读命令分类，请查看文档监控说明               |
| StatSetMin       | 写请求             | 次/秒 | 写命令执行次数，读命令分类，请查看文档监控说明               |
| StatOtherMin     | 其他请求           | 次/秒 | 读写命令之外的命令执行次数，其他命令分类，请查看文档监控说明 |
| BigValueMin      | 大Value请求        | 次/秒 | 请求命令大小超过32KB的执行次数                               |
| SlowQueryMin     | 慢查询             | 次    | 执行时延大于slowlog-log-slower-than配置的命令次数            |
| StatSuccessMin   | 读请求命中         | 次    | 读请求Key存在的个数，对应info命令输出的keyspace_hits指标     |
| StatMissedMin    | 读请求Miss         | 次    | 读请求Key不存在的个数，对应info命令输出的keyspace_misses指标 |
| CmdErrMin        | 执行错误           | 次    | 命令执行错误的次数，例如命令不存在、参数错误等情况           |
| CacheHitRatioMin | 读请求命中率       | %     | Key命中/(Key命中+KeyMiss)，该指标可以反应Cache Miss的情况    |

#### 2.2.3 集群版分片指标信息

| 指标名称         | 指标含义     | 单位  | 指标说明                                                     |
| :--------------- | :----------- | :---- | :----------------------------------------------------------- |
| CpuUsMin         | CPU使用率    | %     | 平均CPU使用率                                                |
| StorageMin       | 内存使用量   | %     | 实际使用内存容量，包含数据和缓存部分                         |
| StorageUsMin     | 内存使用率   | MB    | 实际使用内存和申请总内存之比                                 |
| KeysMin          | Key总个数    | 个    | 实例存储的总Key个数（一级Key）                               |
| ExpiredKeysMin   | key过期数    | 个    | 时间窗内被淘汰的Key个数，对应info命令输出的expired_keys      |
| EvictedKeysMin   | key驱逐数    | 个    | 时间窗内被驱逐的Key个数，对应info命令输出的evicted_keys      |
| QpsMin           | 总请求       | 次/秒 | QPS，命令执行次数                                            |
| StatGetMin       | 读请求       | 次/秒 | 读命令执行次数，读命令分类，请查看文档监控说明               |
| StatSetMin       | 写请求       | 次/秒 | 写命令执行次数，读命令分类，请查看文档监控说明               |
| StatOtherMin     | 其他请求     | 次/秒 | 读写命令之外的命令执行次数，其他命令分类，请查看文档监控说明 |
| SlowQueryMin     | 慢查询       | 次    | 执行时延大于slowlog-log-slower-than配置的命令次数            |
| StatSuccessMin   | 读请求命中   | 次    | 读请求Key存在的个数，对应info命令输出的keyspace_hits指标     |
| StatMissedMin    | 读请求Miss   | 次    | 读请求Key不存在的个数，对应info命令输出的keyspace_misses指标 |
| CmdErrMin        | 执行错误     | 次    | 命令执行错误的次数，例如命令不存在、参数错误等情况           |
| CacheHitRatioMin | 读请求命中率 | %     | Key命中/(Key命中+KeyMiss)，该指标可以反应Cache Miss的情况，当访问为0时，该值为null |

## 3. 输出参数

| 参数名称   | 类型                  | 描述                                                         |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String                | 监控指标                                                     |
| StartTime  | Timestamp             | 数据点起始时间                                               |
| EndTime    | Timestamp             | 数据点结束时间                                               |
| Period     | Integer               | 数据统计周期                                                 |
| DataPoints | Array of PointsObject | 监控数据列表                                                 |
| RequestId  | String                | 唯一请求ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId。 |

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

### 示例1 拉取单个云数据库REDIS的get命令数监控数据示例

拉取某个云数据库REDIS某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&[<公共请求参数>](https://intl.cloud.tencent.com/document/product/248/4478)
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:35:00",
    "EndTime": "2019-06-04 00:40:00",
    "Period": 60,
    "MetricName": "CmdstatGetMin",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-miv64oan"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
  }
}
```

### 示例2 拉取多个云数据库REDIS的数据get命令数监控数据示例

拉取多个云数据库REDIS某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:35:00",
    "EndTime": "2019-06-04 00:40:00",
    "Period": 60,
    "MetricName": "CmdstatGetMin",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-123456"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-1234567"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
  }
}
```

### 示例3 拉取单个云数据库REDIS的实例分片信息get命令数监控数据示例

拉取某个云数据库REDIS实例分片信息某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-1234567
&[<公共请求参数>](https://intl.cloud.tencent.com/document/product/248/4478)
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:35:00",
    "EndTime": "2019-06-04 00:40:00",
    "Period": 60,
    "MetricName": "CmdstatGetNodeMin",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-1234567"
          },{
            "Name": "clusterid",
            "Value": "tdsql-1234567"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
  }
}
```

### 示例4 拉取多个云数据库REDIS的实例分片信息数据get命令数监控数据示例

拉取多个云数据库REDIS实例分片信息某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&Instances.1.Dimensions.1.Name=clusterid
&Instances.1.Dimensions.1.Value=tdsql-1234567
&<公共请求参数>
```

#### 输出示例



```
{
  "Response": {
    "StartTime": "2019-06-04 00:35:00",
    "EndTime": "2019-06-04 00:40:00",
    "Period": 60,
    "MetricName": "CmdstatGetNodeMin",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-1234567"
          },{
            "Name": "clusterid",
            "Value": "tdsql-1234567"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "instanceid",
            "Value": "crs-123456"
          },{
            "Name": "clusterid",
            "Value": "tdsql-123456"
          }
        ],
        "Timestamps": [
          1559579700,
          1559579760,
          1559579820,
          1559579880,
          1559579940,
          1559580000
        ],
        "Values": [
          0,
          0,
          0,
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
  }
}
```