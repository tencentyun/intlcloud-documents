## 1. API Description

API: GetMonitorData<br>
Domain name for API request: monitor.tencentcloudapi.com

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. It is recommended that you spread the call requests over time as much as possible.

To query the monitoring data of TcaplusDB, use the following input parameters:<br>
&Namespace=QCE/TCAPLUS<br>
&Instances.N.Dimensions.0.Name=TableInstanceId<br>
&Instances.N.Dimensions.0.Value=Specific database ID<br>
&Instances.N.Dimensions.1.Name=ApplicationId<br>
&Instances.N.Dimensions.1.Value=Specific application ID<br>

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

| Parameter Name        | Required | Type                                       | Description                                       |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action      | Yes    | String                                   | Common parameter. The value used for this API: GetMonitorData                |
| Version     | Yes    | String                                   | Common parameter. The value used for this API: 2018-07-24                   |
| Region      | No    | String                                   | Common parameter, indicating the region of the instance for which to query monitoring data. For supported regions, please see the [list of regions](https://cloud.tencent.com/document/product/596/39651#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by TcaplusDB |
| Namespace   | Yes    | String                                   | Namespace. Each Tencent Cloud product has a namespace, such as QCE/TCAPLUS             |
| MetricName  | Yes    | String                                   | Metric name. For more information, please see section 2.2                            |
| Instances.N | Yes    | Array of [Instance](https://cloud.tencent.com/document/product/248/30354) | Combination of instance object dimensions                                |
| Period      | No    | Integer                                  | Statistical period for monitoring data in seconds. Default value: 300                    |
| StartTime   | No    | Datetime | Start time, such as "2018-09-22T19:51:23+08:00". Default value: "00:00:00" on the current day |
| EndTime     | No    | Timestamp                                | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime`       |


#### 2.1.2. Dimension parameters

| Parameter Name               | Dimension Name             | Dimension Description          | Format                            |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name  | TableInstanceId              | Database instance ID       | String-type dimension name: TableInstanceId             |
| Instances.N.Dimensions.0.Value | tcaplus-123abc456              | Specific database ID      | Specific instance name, such as tcaplus-123abc456        |
| Instances.N.Dimensions.1.Name  | ApplicationId              | Specific application ID       | String-type dimension name: ApplicationId              |
| Instances.N.Dimensions.1.Value | 123456789              |  Specific application ID     |Specific application ID, such as 123456789  |



### 2.2. Metric name

The statistical granularity (`Period`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `Periods` supported by each API.



#### 2.2.1. Monitoring metrics whose data can be obtained with no installation of monitor agent required

| Metric Name          | Description    | Unit   |
| ------------- | ----- | ---- |
| Avgerror | Average error rate | % |
| Writelatency  | Average write latency | Milliseconds |
| Comerror     | Common error rate | %  |
| Readlatency      | Average read latency | Milliseconds  |
| Volume | Storage capacity | KBytes |
| Syserror  | System error rate | % |
| Writecu | Actual write capacity unit | units/second   |
| Readcu     | Actual read capacity unit | units/second  |


## 3. Output Parameters

| Parameter Name       | Type                    | Description                                       |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String                | Monitoring metric                                     |
| StartTime  | Timestamp             | Data point start time                                  |
| EndTime    | Timestamp             | Data point end time                                  |
| Period     | Integer               | Statistical period                                   |
| DataPoints | Array of PointsObject | Monitoring data list                                   |
| RequestId  | String                | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Examples

### Example 1. Getting the monitoring data of one instance

#### Description

This example shows you how to get the 5-minute average error rate of one TcaplusDB instance for a certain period of time.

#### Input Example

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

&<Common request parameters>
```

#### Output Example

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

### Example 2. Getting the monitoring data of multiple instances

#### Description

This example shows you how to get the 5-minute average error rate of multiple TcaplusDB instances for a certain period of time.

#### Input Example

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
&<Common request parameters>
```

#### Output Example

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