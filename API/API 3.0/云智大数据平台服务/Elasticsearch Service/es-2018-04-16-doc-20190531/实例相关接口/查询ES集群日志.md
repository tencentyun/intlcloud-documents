## 1. 接口描述

接口请求域名： es.tencentcloudapi.com 。

查询用户该地域下符合条件的ES集群的日志

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：es.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/845/30623)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeInstanceLogs |
| Version | 是 | String | 公共参数，本接口取值：2018-04-16 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceId | 是 | String | 集群实例ID |
| LogType | 否 | Integer | 日志类型，默认值为1<br/><li>1, 主日志</li><li>2, 搜索慢日志</li><li>3, 索引慢日志</li><li>4, GC日志</li> |
| SearchKey | 否 | String | 搜索词，支持LUCENE语法，如 level:WARN、ip:1.1.1.1、message:test-index等 |
| StartTime | 否 | String | 日志开始时间，格式为YYYY-MM-DD HH:MM:SS, 如2019-01-22 20:15:53 |
| EndTime | 否 | String | 日志结束时间，格式为YYYY-MM-DD HH:MM:SS, 如2019-01-22 20:15:53 |
| Offset | 否 | Integer | 分页起始值, 默认值为0 |
| Limit | 否 | Integer | 分页大小，默认值为100，最大值100 |
| OrderByType | 否 | Integer | 时间排序方式，默认值为0<br/><li>0, 降序</li><li>1, 升序</li> |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 返回的日志条数|
| InstanceLogList | Array of [InstanceLog](/document/api/845/30634#InstanceLog) | 日志详细信息列表|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询ES集群日志

查询实例最新的主日志

#### 输入示例

```
https://es.tencentcloudapi.com/?Action=DescribeInstanceLogs
&InstanceId=es-f5mwm28u
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "TotalCount": 71633,
    "InstanceLogList": [
      {
        "Time": "2019-01-22T10:45:36.220+08:00",
        "Ip": "10.0.128.65",
        "Level": "INFO",
        "Message": "[o.e.p.o.OPackActionFilter] [1547723102001286009] forbidden request: { ID:cdc62072721547678872c0448c1ecaf9, TYP:MainRequest, USR:null, BRS:false, ACT:cluster:monitor/main, OA:10.0.128.43, IDX:, MET:GET, PTH:/, CNT:<OMITTED, LENGTH=0>, HDR:content-length, EFF:0 } Reason: null"
      },
      {
        "Time": "2019-01-22T10:45:35.730+08:00",
        "Ip": "10.0.128.65",
        "Level": "INFO",
        "Message": "[o.e.p.o.OPackActionFilter] [1547723102001286009] forbidden request: { ID:1a8a5b7ea41a485ebdd769586c1dcdf6, TYP:MainRequest, USR:null, BRS:false, ACT:cluster:monitor/main, OA:10.0.128.73, IDX:, MET:GET, PTH:/, CNT:<OMITTED, LENGTH=0>, HDR:content-length, EFF:0 } Reason: null"
      }
    ],
    "RequestId": "783d9290-dc60-4862-9340-10b632605374"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=DescribeInstanceLogs)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError | 内部错误。 |
| InvalidParameter | 参数错误。 |
