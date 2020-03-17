## 1. 接口描述

接口请求域名： cloudaudit.tencentcloudapi.com 。

用于对操作日志进行检索，便于用户进行查询相关的操作信息。

默认接口请求频率限制：200次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://intl.cloud.tencent.com/document/api/1021/34192)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：LookUpEvents。 |
| Version | 是 | String | 公共参数，本接口取值：2019-03-19。 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| EndTime | 是 | Integer | 结束时间 |
| StartTime | 是 | Integer | 开始时间 |
| LookupAttributes.N | 否 | Array of [LookupAttribute](https://intl.cloud.tencent.com/document/api/1021/34209#LookupAttribute) | 检索条件 |
| MaxResults | 否 | Integer | 返回日志的最大条数 |
| NextToken | 否 | String | 查看更多日志的凭证 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Events | Array of [Event](https://intl.cloud.tencent.com/document/api/1021/34209#Event) | 日志集合|
| ListOver | Boolean | 日志集合是否结束|
| NextToken | String | 查看更多日志的凭证|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 日志检索

用于对操作日志进行检索，便于用户进行查询相关的操作信息。

#### 输入示例

```
https://cloudaudit.tencentcloudapi.com/?Action=LookUpEvents
&EndTime=1553056687
&LookupAttributes.0.AttributeKey=AccessKeyId
&LookupAttributes.0.AttributeValue=AKID7JETaYT3IAmutX0vXCcy4q90zJNvlVZf
&StartTime=1553056487
&<公共请求参数>
```

#### 输出示例

```
{
    "Response": {
        "Events": [
            {
                "CloudAuditEvent": "{"actionType":"Read","apiErrorCode":"","apiErrorMessage":"","apiVersion":"2.0","errorCode":0,"errorMessage":"permission verify","eventID":"e92a92fc259c4a9333d2a7ce64d1ef201","eventName":"LookupEvents","eventRegion":"ap-guangzhou","eventSource":"cloudaudit.api.tencentyun.com/v2/index.php","eventTime":"2019-03-20 12:36:27","eventType":"ConsoleCall","eventVersion":2,"httpMethod":"POST","region":"","requestID":"15936031437374_1553056587.6815_v2","requestParameters":"{"Action":"LookupEvents","EndTime":"1553097599","MaxResults":"10","Nonce":"36881","Region":"gz","RequestClient":"SDK_NODEJS_0.2.1","RequestOperator":"1150691759","RequestSource":"MC","SecretId":"AKID7JETaYT3IAmutX0vXCcy4q90zJNvlVZf","StartTime":"1552406400","Timestamp":"1553056583","Token":"147d2c5b0319541a13d9fe6ceb5af2aae9b67f6610001","seqId":"cdb9c38c-7031-bb13-6a9c-cd7641734c8f"}","resourceName":"","resourceType":"cloudaudit","resources":"","sourceIPAddress":"59.37.125.124","userAgent":"","userIdentity":{"userName":"root","type":"Root","secretId":"AKID7JETaYT3IAmutX0vXCcy4q90zJNvlVZf","accountId":1150691759,"principalId":1150691759,"sessionContext":{"expireTime":"2019-03-20 13:04:46","hasPolicyFilter":0,"extraInfo":"","interfaceName":"","ownerUin":1150691759,"ua":"27513f02ea3ab649f0cacb6476df54eb","mfa":0,"userIp":"59.37.125.124","mfaExpireTime":"2019-03-20 12:34:46","uin":1150691759,"token":"147d2c5b0319541a13d9fe6ceb5af2aae9b67f6610001","appId":1251840716,"policyFilter":""}}}",
                "EventId": "e92a92fc259c4a9333d2a7ce64d1ef201",
                "EventName": "LookupEvents",
                "EventTime": "2019-03-20 12:36:27",
                "SecretId": "AKID7JETaYT3IAmutX0vXCcy4q90zJNvlVZf",
                "ErrorCode": 0,
                "RequestID": "15936031437374_1553056587.6815_v2",
                "AccountID": 1150691759,
                "SourceIPAddress": "59.37.125.124",
                "EventSource": "cloudaudit.api.tencentyun.com/v2/index.php",
                "EventRegion": "ap-guangzhou",
                "Resources": {
                    "ResourceName": "",
                    "ResourceType": "cloudaudit"
                },
                "Username": "root",
                "ResourceTypeCn": "云审计",
                "EventNameCn": "检索日志"
            }
        ],
        "NextToken": "DnF1ZXJ5VGhlbkZldGNoDwAAAAAAACBuFjNoRHJ5YTd4U1B5YWY4c1ZmMmxBQWcAAAAAAAAgnBZZZkZoYy04LVJJeVpJNnZJS2hIVTdRAAAAAAAAI1QWYk5mQmZXTzhTWXFNZjFMVlhHY1RjdwAAAAAAAB9sFmhZbV8xbm1FUXE2NGVDQndWSlNoMncAAAAAAAAd9BZOelN1aGMycFNydUVEQ0dQbzdCcEZBAAAAAAAALroWMTh4c00xalhRbk9wR0NsYWZvV20tQQAAAAAAACCdFllmRmhjLTgtUkl5Wkk2dklLaEhVN1EAAAAAAAAuuRYxOHhzTTFqWFFuT3BHQ2xhZm9XbS1BAAAAAAAAIJ4WWWZGaGMtOC1SSXlaSTZ2SUtoSFU3UQAAAAAAAB81FnN5aTBfTWJKU25HdXZuMWxsRkdJZ3cAAAAAAAApMhZ1UjdybjlCY1NRYUZVYWRub2x4YW9RAAAAAAAAHzQWc3lpMF9NYkpTbkd1dm4xbGxGR0lndwAAAAAAAB31Fk56U3VoYzJwU3J1RURDR1BvN0JwRkEAAAAAAAAfbRZoWW1fMW5tRVFxNjRlQ0J3VkpTaDJ3AAAAAAAAH24WaFltXzFubUVRcTY0ZUNCd1ZKU2gydw==",
        "ListOver": true,
        "RequestId": "91e2998d-edc0-4ba0-a76d-cebbbfd99391"
    }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=LookUpEvents)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.SearchError | 内部错误，请联系开发人员 |
| InvalidParameter.Time | 必须包含开始时间和结束时间，且必须为整形时间戳（精确到秒） |
| InvalidParameterValue.MaxResult | 单次检索支持的最大返回条数是50 |
| InvalidParameterValue.Time | 开始时间不能大于结束时间 |
| InvalidParameterValue.attributeKey | AttributeKey的有效取值范围是:RequestId、EventName、ReadOnly、Username、ResourceType、ResourceName和AccessKeyId |
| LimitExceeded.OverTime | 检索支持的有效时间范围是7天 |
