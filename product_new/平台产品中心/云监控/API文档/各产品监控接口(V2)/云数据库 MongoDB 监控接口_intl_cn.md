## 1. 接口描述

接口：GetMonitorData
接口请求域名： monitor.tencentcloudapi.com

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库MongoDB监控数据，入参取值如下：
&Namespace= QCE/CMONGO
&Instances.N.Dimensions.0.Name=target
&Instances.N.Dimensions.0.Value=视查询维度而定

下面来说明下Instances.N.Dimensions.0.Value的取值。 腾讯云提供的MongoDB是集群服务，通过本API可以查询“整个集群”、“某个副本集”、“某个节点”三个维度的监控数据。 其中： “整个集群”代表了您所购买的某一个MongoDB实例，这个维度可以查询整个实例的读写请求次数、容量使用率、超时请求等。 “某个副本集”维度可查询集群下的某一个副本集内部的容量使用率和主从延迟。副本集实例本身只包含一个副本集，分片实例的每一片都是一个副本。 “某个节点”维度可以查询集群内的任意节点的CPU、内存等信息。

### dimensions.0.value 取值参照表

| 取值类型 | 取值示例                                                     | 描述                                                         |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 实例ID   | cmgo-6ielucen                                                | 实例ID一个MongoDB实例的唯一标识；可以在[MongoDB控制台](https://console.cloud.tencent.com/mongodb)查询到；或者调用MognoDB的API也可以获取 |
| 副本集ID | cmgo-6ielucen_0cmgo-6ielucen_2                               | 在实例ID后面拼接 “_索引号”可以得到副本集ID；“索引号”从0开始，最大值为副本集个数-1；副本集实例只有一个副本集，所以固定拼接“_0”即可；分片实例有多个片，每一片都是副本集，举例：第3个片的副本集ID就是拼接“_2” |
| 节点ID   | cmgo-6ielucen_0-node-primarycmgo-6ielucen_1-node-slave0cmgo-6ielucen_3-node-slave2 | 在副本集ID后面拼接“-node-primary”得到该副本集的主节点ID；拼接“-node-slave从节点索引号”可得到对应的从节点的ID，“从节点索引号”从0开始，最大值为从节点个数-1 |

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1)页面。

### 2.1输入参数

#### 2.1.1 输入参数总览

| 参数名称    | 是否必选 | 类型                                                         | 描述                                                         |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action      | 是       | String                                                       | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String                                                       | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String                                                       | 公共参数，表示查询的是哪个地域实例的监控数据；可查看MongoDB支持的 [地域列表](https://intl.cloud.tencent.com/document/product/240/32141#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) |
| Namespace   | 是       | String                                                       | 命名空间，每个云产品会有一个命名空间，如MongoDB命名空间： QCE/CMONGO （API 3.0接口版本的必须是大写） |
| MetricName  | 是       | String                                                       | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合                                           |
| Period      | 否       | Integer                                                      | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp                                                    | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp                                                    | 结束时间，默认为当前时间。 endTime不能小于startTime          |

#### 2.1.2 各维度对应参数总览

| 参数名称                       | 维度名称 | 维度解释       | 格式                                                         |
| :----------------------------- | :------- | :------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | target   | 入参为target   | 输入String类型维度名称，如：target                           |
| Instances.N.Dimensions.0.Value | target   | 视查询维度而定 | 请参考 [取值参照表](https://intl.cloud.tencent.com/document/product/248/35671#dimensions.0.value-.E5.8F.96.E5.80.BC.E5.8F.82.E7.85.A7.E8.A1.A8) 取值 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标             | 含义                                   | 单位 | 集群/实例 | dimensions.0.value取值 |
| :--------------- | :------------------------------------- | :--- | :-------- | :--------------------- |
| Inserts          | 单位时间内写入次数                     | 次   | 集群/实例 | 实例ID                 |
| Reads            | 单位时间内读取次数                     | 次   | 集群/实例 | 实例ID                 |
| Updates          | 单位时间内更新次数                     | 次   | 集群/实例 | 实例ID                 |
| Deletes          | 单位时间内删除次数                     | 次   | 集群/实例 | 实例ID                 |
| Counts           | 单位时间内ount次数                     | 次   | 集群/实例 | 实例ID                 |
| Aggregates       | 单位时间内aggregates次数               | 次   | 集群/实例 | 实例ID                 |
| ClusterDiskusage | 集群容量使用率                         | %    | 集群/实例 | 实例ID                 |
| Success          | 单位时间内成功请求次数                 | 次   | 集群/实例 | 实例ID                 |
| Delay10          | 单位时间内成功请求延迟在10ms-50ms次数  | 次   | 集群/实例 | 实例ID                 |
| Delay50          | 单位时间内成功请求延迟在50ms-100ms次数 | 次   | 集群/实例 | 实例ID                 |
| Delay100         | 单位时间内成功请求延迟在100ms以上次数  | 次   | 集群/实例 | 实例ID                 |
| ReplicaDiskusage | 副本集容量使用率                       | %    | 副本集    | 副本集ID               |
| Slavedelay       | 主从单位时间内平均延迟                 | 秒   | 副本集    | 副本集ID               |
| Cpuusage         | CPU使用率                              | %    | 节点      | 节点ID                 |
| Memusage         | 内存使用率                             | %    | 节点      | 节点ID                 |
| Qr               | Read请求等待队列中的个数               | 个   | 节点      | 节点ID                 |
| Qw               | Write请求等待队列中的个数              | 个   | 节点      | 节点ID                 |
| Conn             | 连接数                                 | 个   | 节点      | 节点ID                 |
| Netin            | 网络入流量                             | MB/s | 节点      | 节点ID                 |
| Netout           | 网络出流量                             | MB/s | 节点      | 节点ID                 |

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

## 5. 示例

### 示例1 拉取单个云数据库MongoDB的单位时间内写入次数监控数据示例

拉取某个云数据库MongoDB某段时间内统计周期为60秒的单位时间内写入次数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/CMONGO
&MetricName=Inserts
&Period=60
&StartTime=2019-06-17T20:20:00+08:00
&EndTime=2019-06-178T20:25:00+08:00
&Instances.0.Dimensions.0.Name=target
&Instances.0.Dimensions.0.Value=cmgo-g9c1234
&[<公共请求参数>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### 输出示例

```
{
  "Response": {
    "StartTime": "2019-06-17 20:20:00",
    "EndTime": "2019-06-17 20:25:00",
    "Period": 60,
    "MetricName": "Inserts",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "target",
            "Value": "cmgo-g9c1234"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
    "RequestId": "d133e798-4d13-4ecf-af21-cce93967811c"
  }
}
```

### 示例2 拉取多个云数据库MongoDB的单位时间内写入次数监控数据示例

拉取多个云数据库MongoDB某段时间内统计周期为60秒的单位时间内写入次数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CMONGO
&MetricName=Inserts
&Period=60
&StartTime=2019-06-17T20:20:00+08:00
&EndTime=2019-06-178T20:25:00+08:00
&Instances.0.Dimensions.0.Name=target
&Instances.0.Dimensions.0.Value=cmgo-g9c1234
&Instances.1.Dimensions.0.Name=target
&Instances.1.Dimensions.0.Value=cmgo-g9c12345
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "StartTime": "2019-06-17 20:20:00",
    "EndTime": "2019-06-17 20:25:00",
    "Period": 60,
    "MetricName": "Inserts",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "target",
            "Value": "cmgo-g9c1234"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
            "Name": "target",
            "Value": "cmgo-g9c12345"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
    "RequestId": "d133e798-4d13-4ecf-af21-cce93967811c"
  }
}
```