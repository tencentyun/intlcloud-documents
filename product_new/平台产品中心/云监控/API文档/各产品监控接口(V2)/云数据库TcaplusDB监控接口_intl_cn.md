## 1. 接口描述

接口：GetMonitorData<br>
接口请求域名： monitor.tencentcloudapi.com

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询游戏数据库 TcaplusDB监控数据，入参取值如下：<br>
&Namespace=QCE/TCAPLUS<br>
&Instances.N.Dimensions.0.Name=TableInstanceId<br>
&Instances.N.Dimensions.0.Value=数据库的具体ID<br>
&Instances.N.Dimensions.1.Name=ApplicationId<br>
&Instances.N.Dimensions.1.Value=应用申请的具体ID<br>

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478)页面。

### 2.1输入参数

| 参数名称    | 是否必选 | 类型              | 描述                                                         |
| ----------- | -------- | ----------------- | ------------------------------------------------------------ |
| Action      | 是       | String            | 公共参数，本接口取值：GetMonitorData                         |
| Version     | 是       | String            | 公共参数，本接口取值： 2018-07-24                            |
| Region      | 否       | String            | 公共参数，表示查询的是哪个地域实例的监控数据                 |
| Namespace   | 是       | String            | 命名空间，每个云产品会有一个命名空间,如：QCE/TCAPLUS         |
| MetricName  | 是       | String            | 指标名称，具体名称见2.2                                      |
| Instances.N | 是       | Array of Instance | 实例对象的维度组合                                           |
| Period      | 否       | Integer           | 监控统计周期。默认为取值为300，单位为s                       |
| StartTime   | 否       | Timestamp         | 起始时间，如"2018-09-22T19:51:23+08:00"。 默认时间为当天的”00:00:00” |
| EndTime     | 否       | Timestamp         | 结束时间，默认为当前时间。 EndTime不能小于StartTime          |


#### 2.1.2 各维度对应参数总览

| 参数名称               | 维度名称             | 维度解释          | 格式                            |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name  | TableInstanceId              | 数据库实例 ID       | String类型维度名称：TableInstanceId             |
| Instances.N.Dimensions.0.Value | tcaplus-123abc456              | 数据库的具体ID      | 具体实例名称，如:tcaplus-123abc456        |
| Instances.N.Dimensions.1.Name  | ApplicationId              | 应用申请的具体ID       | String类型维度名称：ApplicationId              |
| Instances.N.Dimensions.1.Value | 123456789              |  应用申请的具体ID     |具体应用申请的ID，如:123456789  |



### 2.2 指标名称

每个指标的统计粒度（Period）可取值不一定相同，可通过DescribeBaseMetrics接口获取每个接口支持的统计粒度。



#### 2.2.1 不需要安装监控agent，就能获取数据的监控指标

| 指标名称          | 含义    | 单位   |
| ------------- | ----- | ---- |
| Avgerror | 平均错误率 | % |
| Writelatency  | 平均写时延 | 微秒 |
| Comerror     | 一般错误率 | %  |
| Readlatency      | 平均读时延 | 微秒  |
| Volume | 存储容量 | KBytes |
| Syserror  | 系统错误率 | % |
| Writecu | 实际写容量单位 | 个/秒   |
| Readcu     | 实际读容量单位 | 个/秒  |


## 3. 输出参数

| 参数名称       | 类型                    | 描述                                       |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String                | 监控指标                                     |
| StartTime  | Timestamp             | 数据点起始时间                                  |
| EndTime    | Timestamp             | 数据点结束时间                                  |
| Period     | Integer               | 数据统计周期                                   |
| DataPoints | Array of PointsObject | 监控数据列表                                   |
| RequestId  | String                | 唯一请求ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId。 |

## 4. 示例

### 示例1 拉取单个实例监控数据示例

#### 场景描述

拉取单个游戏数据库 TcaplusDB某段时间内统计周期为5分钟的平均错误率监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/TCAPLUS
&MetricName=Avgerror
&Period=300
&StartTime=2018-08-24T10:40:23+08:00
&EndTime=2018-08-24T10:50:23+08:00
&Instances.0.Dimensions.0.Name=TableInstanceId
&Instances.0.Dimensions.0.Value=tcaplus-123abc456
&Instances.0.Dimensions.1.Name=ApplicationId
&Instances.0.Dimensions.1.Value=123456789

&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc456"
          },
          {
            "Name": "ApplicationId",
            "Value": "123456789"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          2.566,
          2.283,
          6.316
        ]
      }
    ],
    "EndTime": "2018-08-24 10:50:00",
    "MetricName": "Avgerror",
    "Period": 300,
    "RequestId": "d96ec542-6547-4af2-91ac-fee85c1b8b85",
    "StartTime": "2018-08-24 10:40:00"
  }
}
```

### 示例2 拉取多个实例监控数据示例

#### 场景描述

拉取多个游戏数据库 TcaplusDB某段时间内统计周期为5分钟的平均错误率监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/TCAPLUS
&MetricName=Avgerror
&Period=300
&StartTime=2018-09-22T10:40:23+08:00
&EndTime=2018-09-22T10:50:23+08:00
&Instances.0.Dimensions.0.Name=TableInstanceId
&Instances.0.Dimensions.0.Value=tcaplus-123abc456
&Instances.0.Dimensions.1.Name=ApplicationId
&Instances.0.Dimensions.1.Value=123456789
&Instances.1.Dimensions.0.Name=TableInstanceId
&Instances.1.Dimensions.0.Value=tcaplus-123abc789
&Instances.1.Dimensions.1.Name=ApplicationId
&Instances.1.Dimensions.1.Value=987654321
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc456"
          },
          {
            "Name": "ApplicationId",
            "Value": "123456789"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          2,
          2,
          6
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc789"
          },
          {
            "Name": "ApplicationId",
            "Value": "987654321"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          3,
          3,
          6
        ]
      }
    ],
    "EndTime": "2018-09-22 10:50:00",
    "MetricName": "Avgerror",
    "Period": 300,
    "RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
    "StartTime": "2018-09-22 11:00:00"
  }
}
```