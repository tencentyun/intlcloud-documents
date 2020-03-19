## 1. 接口描述

接口：GetMonitorData<br>
接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询对象存储监控数据，入参取值如下：<br>
&Namespace=QCE/COS<br>
&Instances.N.Dimensions.0.Name=appid<br>
&Instances.N.Dimensions.0.Value 为主账号的 APPID<br>
&Instances.N.Dimensions.1.Name=bucket<br>
&Instances.N.Dimensions.1.Value 为存储桶名称 <br>

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/248/4478#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1) 文档。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称    | 是否必选 | 类型                                                         | 描述                                                         |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action      | 是       | String                                                       | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String                                                       | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String                                                       | 公共参数，表示查询的是哪个地域实例的监控数据。支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/zh/document/product/213/15692) |
| Namespace   | 是       | String                                                       | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如：    QCE/COS |
| MetricName  | 是       | String                                                       | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合                                           |
| Period      | 否       | Integer                                                      | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp                                                    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp                                                    | 结束时间，默认为当前时间。 endTime 不能小于 startTime        |

#### 2.1.2 各维度对应参数总览

| 参数名称                        | 维度名称 | 维度解释     | 格式                                    |
| ------------------------------- | -------- | ------------ | --------------------------------------- |
| &Instances.N.Dimensions.0.Name  | appid    | 主账号 APPID | String 类型                             |
| &Instances.N.Dimensions.0.Value | appid    | 主账号 APPID | 主账号 APPID，如 1250000000             |
| &Instances.N.Dimensions.1.Name  | bucket   | 存储桶名称   | String 类型                             |
| &Instances.N.Dimensions.1.Value | bucket   | 存储桶名称   | 存储桶名称，如 examplebucket-1250000000 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

#### 存储类

存储类指标支持的最小统计周期（period）为300，并支持使用3600、86400为拉取周期。

| 指标名称（metricName） | 含义              | 单位 |
| ---------------------- | ----------------- | ---- |
| StdStorage             | 标准存储-存储空间 | MB   |
| SiaStorage             | 低频存储-存储空间 | MB   |
| NelStorage             | 近线存储-存储空间 | MB   |
| ArcStorage             | 归档存储-存储空间 | MB   |

#### 流量类

流量类指标支持的最小统计周期（period）为60，并支持使用300、3600、86400为拉取周期。

| 指标名称（metricName） | 含义          | 单位 |
| ---------------------- | ------------- | ---- |
| InternetTraffic        | 外网流量      | B    |
| InternalTraffic        | 内网流量      | B    |
| CdnOriginTraffic       | CDN  回源流量 | B    |
| InboundTraffic         | 上传流量      | B    |

#### 数据读取类

数据读取类指标支持的最小统计周期（period）为60，并支持使用300、3600、86400为拉取周期。

| 指标名称（metricName） | 含义         | 单位 |
| ---------------------- | ------------ | ---- |
| StdRetrieval           | 标准数据读取 | B    |
| IaRetrieval            | 低频数据读取 | B    |
| NlRetrieval            | 近线数据读取 | B    |

#### 请求类

请求类指标支持的最小统计周期（period）为60，并支持使用 300、3600、86400为拉取周期。

| 指标名称（metricName） | 含义           | 单位 |
| ---------------------- | -------------- | ---- |
| StdReadRequests        | 标准存储读请求 | 次数 |
| StdWriteRequests       | 标准存储写请求 | 次数 |
| IaReadRequests         | 低频存储读请求 | 次数 |
| IaWriteRequests        | 低频存储写请求 | 次数 |
| NlReadRequests         | 近线存储读请求 | 次数 |
| NlWriteRequests        | 近线存储写请求 | 次数 |

#### 返回码类

| 指标名称（metricName） | 含义        | 单位 |
| ---------------------- | ----------- | ---- |
| 2xxResponse            | 2xx  状态码 | 次数 |
| 3xxResponse            | 3xx  状态码 | 次数 |
| 4xxResponse            | 4xx  状态码 | 次数 |
| 5xxResponse            | 5xx  状态码 | 次数 |

## 3. 输出参数

| 参数名称   | 类型                  | 描述                                                         |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String                | 监控指标                                                     |
| StartTime  | Timestamp             | 数据点起始时间                                               |
| EndTime    | Timestamp             | 数据点结束时间                                               |
| Period     | Integer               | 数据统计周期                                                 |
| DataPoints | Array of PointsObject | 监控数据列表                                                 |
| RequestId  | String                | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId |

## 4. 错误码表

| 错误代码 | 错误描述       | 英文描述                             |
| -------- | -------------- | ------------------------------------ |
| -502     | 资源不存在     | OperationDenied.SourceNotExists      |
| -503     | 请求参数有误   | InvalidParameter                     |
| -505     | 参数缺失       | InvalidParameter.MissingParameter    |
| -507     | 超出限制       | OperationDenied.ExceedLimit          |
| -509     | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513     | DB操作失败     | InternalError.DBoperationFail        |

## 5. 示例

### 示例1

拉取某个对象存储某段时间内统计周期为300秒的标准存储-存储空间监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=appid
&Instances.0.Dimensions.0.Value=1250000000
&Instances.0.Dimensions.1.Name=bucket
&Instances.0.Dimensions.1.Value=examplebucket-1250000000 
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "5xxResponse",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000000"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000000"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-022d10eb91fc"
  }
}
```

### 示例2 

拉取多个对象存储某段时间内统计周期为300秒的标准存储-存储空间监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=appid
&Instances.0.Dimensions.0.Value=1250000000
&Instances.0.Dimensions.1.Name=bucket
&Instances.0.Dimensions.1.Value=examplebucket-1250000000
&Instances.1.Dimensions.0.Name=appid
&Instances.1.Dimensions.0.Value=1250000001
&Instances.1.Dimensions.1.Name=bucket
&Instances.1.Dimensions.1.Value=examplebucket-1250000001 
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "5xxResponse",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000000"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000000"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000001"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000001"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-022d10eb91fc"
  }
}
```