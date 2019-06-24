## 1. API Description

Domain name: monitor.api.qcloud.com
API: GetMonitorData

Cloud Redis Store (CRS) is a reliable and highly available Redis service platform based on Tencent Cloud's years of experience in distributed cache and Redis business demands. To learn more, see <a href="/doc/product/239/产品介绍" title="Product Introduction">Cloud Redis Store Introduction</a>.

This API (GetMonitorData) is used to query the monitoring data of CRS. The values for input parameters are as follows:
namespace:  qce/redis
dimensions.0.name=redis_uuid
Dimensions.0.value is instance uuid

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters are also required when calling API. For more information, please see <a href="/doc/api/405/公共请求参数" title="Common Request Parameters">Common Request Parameters</a>. The Action field for this API is GetMonitorData.

## 2.1. Input Parameters

| Parameter Name               | Required   | Type       | Input Content       | Description                                       |
| ------------------ | ---- | -------- | ---------- | ---------------------------------------- |
| namespace          | Yes    | String   | qce/redis  | Namespace. Every cloud product has a namespace. You can see the specific name in Input Content column.           |
| metricName         | Yes    | String   | Specific metric name    | Metric name. You can see the specific name in 2.2                            |
| dimensions.0.name  | Yes    | String   | redis_uuid | Input parameter must be redis_uuid                          |
| dimensions.0.value | Yes    | String   | Specific uuid    | Enter Redis instance id, i.e. instance ID, such as crs-ifmymj41. It can be queried with the API [Query CRS Instance List](https://intl.cloud.tencent.com/document/api/239/1384) |
| period             | No    | Int      | 60/300  | Period for collecting monitoring data. Most metrics support a statistical granularity of 60s while some metrics only support a statistical granularity of 300s. Statistical granularity varies with metrics.  Refer to the list of metric details in 2.2 when entering parameters.  |
| startTime          | No    | Datetime | Start time       | Start time. For example, "2016-01-01 10:25:00".   The start time is "00:00:00" in that day by default  |
| endTime            | No    | Datetime | End time       | End time. Current time by default.   endTime cannot be earlier than startTime       |


### 2.2 Metric Name

| Name            | Collecting Method (Meaning in Linux)                         | Metric Statistical Method                    | Unit    |
| ----------- | ---------------- | ---------------------------------------- | ------------------------- |
| cache_hit_ratio  | Collect the value of keyspace_misses and keyspace_hits every minute and using the following formula to calculate: (1- keyspace_misses/keyspace_hits)* 100%.  This metric is no longer maintained | Collected every minute and the 5 minutes granularity data is the average value of the last 5 minutes  | %     |
| cmdstat_get      | Requests of get command within 1 minute                           | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_getbit   | Requests of getbit command within 1 minute                        | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_getrange | Requests of getrange command within 1 minute                      | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hget     | Requests of hget command within 1 minute                          | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hgetall  | Requests of hgetall command within 1 minute                       | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hmget    | Requests of hmget command within 1 minute                         | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hmset    | Requests of hmset command within 1 minute                         | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hset     | Requests of hset command within 1 minute                         | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_hsetnx   | Requests of hsetnx command within 1 minute                        | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_lset     | Requests of lset command within 1 minute                          | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_mget     | Requests of mget command within 1 minute                          | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_mset     | Requests of mset command within 1 minute                          | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_msetnx   | Requests of msetnx command within 1 minute                        | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
 | cmdstat_set      | Requests of set command within 1 minute                           | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_setbit   | Requests of setbit command within 1 minute                       | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_setex    | Requests of setex command within 1 minute                         | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
 | cmdstat_setnx    | Requests of setnx command within 1 minute                         | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| cmdstat_setrange | Requests of setrange command within 1 minute                      | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| qps              | Total requests of command within 1 minutes divided by 60                             | Collected every minute and the 5 minutes granularity data is the average value of the last 5 minutes  | times/min  |
| connections      | Total connections within 1 minute                                | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times     |
| cpu_us           | Percentage of time during which the CPU is occupied, which is calculated by obtaining data /proc/stat         | ollected every minute and the 5 minutes granularity data is the average value of the last 5 minutes | %     |
| in_flow          | Total private inbound traffic within 1 minute                                | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | MB/min |
| keys             | Maximum number of keys within 1 minute                            | Collected every minute. The 5 minutes granularity is the maximum value over the last 5 minutes | keys     |
| out_flow         | Total private outbound traffic within 1 minute                                | Collected every minute. The 5 minutes granularity is the maximum value over the last 5 minutes    | MB/min |
| stat_get         | Total get command requests within 1 minute, including get, hget, hgetall, hmget, mget, getbit, getrange  | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| stat_set         | Total set command requests within 1 minute, including set, hset, hmset, hsetnx, lset, mset, msetnx, setbit, setex, setrange, setnx | Collected every minute and the 5 minutes granularity data is the sum of requests in last 5 minutes   | times/min  |
| storage          | Maximum value of the occupied capacity within 1 minute                            | Collected every minute. The 5 minutes granularity is the maximum value over the last 5 minutes | MB/min |
| storage_us       | Maximum percentage of the occupied capacity within 1 minute                         | Collected every minute. The 5 minutes granularity is the maximum value over the last 5 minutes | %     |


## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | -------- | ------------------- |
| code | Int | Error code. 0: successful, and the other values: failed  0: Successful. Other values: Failed |
| message | String | Return message |
| startTime | Datetime | Start time |
| endTime | Datetime | End time |
| metricName | String | Metric name |
| period | Int | Monitoring statistical cycle |
| dataPoints | Array | Monitoring data list |


## 4. Error Codes

| Error Code |  Description | Error Message |
| ---- | ------- | ------------------------------------ |
| -502 | Resource does not exist | OperationDenied.SourceNotExists |
| -503 | Invalid request parameter | InvalidParameter |
| -505 | Parameter is missing | InvalidParameter.MissingParameter |
| -507 | Limit is exceeded | OperationDenied.ExceedLimit |
| -509 | Invalid dimension group | InvalidParameter.DimensionGroupError |
| -513 | DB operation failed | InternalError.DBoperationFail |

## 5. Example

Input

<pre>
https://monitor.api.qcloud.com/v2/index.php?
</td><td> For details, please refer to the <a href="/doc/api/405/公共请求参数" title="公共请求参数">Comman request parameters</a>.
&namespace=qce/redis
&metricName=cache_hit_ratio
&dimensions.0.name=redis_uuid
&dimensions.0.value=crs-ifmymj41
&startTime=2016-06-28 14:10:00
&endTime=2016-06-28 2:20:00 PM
</pre>

Output

```shell
{
	"code": 0,
	"message": "",
	"metricName": "cache_hit_ratio",
	"startTime": "2016-06-28 14:10:00",
	"endTime": "2016-06-28 14:20:00",
	"period": 300,
	"dataPoints": [
		50,
		40,
		30
	]
}
```
