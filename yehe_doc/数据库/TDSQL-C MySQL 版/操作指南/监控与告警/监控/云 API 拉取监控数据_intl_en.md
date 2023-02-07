This document describes how to pull the monitoring metric data of TDSQL-C for MySQL through TencentCloud API. For detailed directions and more examples, see [GetMonitorData](https://www.tencentcloud.com/document/product/248/33881).

## API description
This API is used to get the monitoring data of TDSQL-C for MySQL by passing in its namespace, object dimension, and monitoring metric.
API call rate limit: 20 calls/sec (1,200 calls/minute). A single request can get the data of up to 10 instances for up to 1,440 data points.
This API may fail due to the rate limit if you need to call many metrics and objects. We recommend you distribute call requests across a period of time.
Default API request rate limit: 20 requests/sec.

## Input parameters
The list below only contains API request parameters and some common parameters. For a complete common parameter list, see [Common Params](https://www.tencentcloud.com/document/product/248/33876).

| Parameter Name  | Required | Type   | Description       |
|---------|---------|---------|---------|
| Action      | Yes    | String                                   | Common parameter. The value used for this API: GetMonitorData.                |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://www.tencentcloud.com/document/product/248/33876#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Namespace | Yes | String | Namespace, such as `QCE/cynosdb_mysql`. For more information, see [TDSQL-C for MySQL Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/37383). |
| MetricName | Yes | String | Metric name, such as `CPUUsagerate` (CPU utilization). You can pull the data of one single metric at a time. |
| Instances.N | Yes | Array of Instance | Dimension combination of instance object in the format of `key-value` pair. Different types of instances have completely different fields. For the dimension combination of TDSQL-C for MySQL, see [TDSQL-C for MySQL Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/37383). |
| Period | No 	| Integer | Statistical period for monitoring data in seconds, such as `60`. Default value: `300`. |
| StartTime | No	 | Timestamp ISO8601 | Start time, such as `2021-07-15T19:51:23+08:00`. |
| EndTime | No | Timestamp ISO8601 | End time, such as `2021-07-15T20:51:23+08:00`. It is the current time by default and cannot be before `StartTime`. |

## Output parameters

| Parameter | Type | Description |
|---------|---------|---------|
| Period | Integer | 	Statistical period |
| MetricName | String | Metric name |
| DataPoints | Array of DataPoint | Array of data points |
| StartTime | Timestamp ISO8601 | Start time |
| EndTime | Timestamp ISO8601 | End time |
| RequestId | String | A unique request ID, which is returned for each request and is required for troubleshooting. |

## Examples
This example shows you how to get the 5-minute CPU utilization monitoring data of a TDSQL-C for MySQL instance in a specific period of time.
**Sample input**
```
POST / HTTP/1.1
Host: monitor.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: GetMonitorData
<Common request parameters>

{
    "Namespace": "QCE/cynosdb_mysql",
    "MetricName": "CPuUsageRate",
    "Period": 3600,
    "Instances": [
        {
            "Dimensions": [
                {
                    "Name": "InstanceId",
                    "Value": "cynosdbmysql-ins-edpn3t6b"
                }
            ]
        }
    ],
    "StartTime": "2022-07-15T10:00:00",
    "EndTime": "2022-07-15T15:00:00"
}
```
**Sample output**
```
{
  "Response": {
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "InstanceId",
            "Value": "cynosdbmysql-ins-edpn3t6b"
          }
        ],
        "Timestamps": [
          1657850400,
          1657854000,
          1657857600,
          1657861200,
          1657864800
        ],
        "Values": [
          0.26,
          0.24,
          0.23,
          0.26,
          0.24
        ]
      }
    ],
		"EndTime": "2022-07-15 15:00:00",
		"MetricName": "CPuUsageRate",
		"Period": 3600,
    "RequestId": "71c72744-bec5-49d0-b42c-433609ab4166"
		 "StartTime": "2022-07-15 10:00:00"
  }
}
```

