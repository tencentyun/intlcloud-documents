## 1. API Description

API domain name: cloudaudit.tencentcloudapi.com.

This API is used to search for operation logs to help query relevant operation information.

Default API request rate limit: 200 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/1021/34192).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: LookUpEvents. |
| Version | Yes | String | Common parameter. The value used for this API: 2019-03-19. |
| Region | Yes | String | Common parameter. For more information, please see the [list of regions](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| EndTime | Yes | Integer | End time |
| StartTime | Yes | Integer | Start time |
| LookupAttributes.N | No | Array of [LookupAttribute](https://intl.cloud.tencent.com/document/api/1021/34209#LookupAttribute) | Filter |
| MaxResults | No | Integer | Maximum number of logs to be returned |
| Mode | No | String | CloudAudit mode. Valid values: standard (standard mode), quick (expedited mode); Default value: standard.|
| NextToken | No | String | Credential for viewing more logs |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Events | Array of [Event](https://intl.cloud.tencent.com/document/api/1021/34209#Event) | Logset |
| ListOver | Boolean | Whether the logset ends |
| NextToken | String | Credential for viewing more logs |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Searching for logs

This example shows you how to search for operation logs to help query relevant operation information.

#### Input sample code

```
https://cloudaudit.tencentcloudapi.com/?Action=LookUpEvents
&EndTime=1553056687
&LookupAttributes.0.AttributeKey=AccessKeyId
&LookupAttributes.0.AttributeValue=AKID7JETaYT3IAmutX0vXCcy4q90zJNvlVZf
&StartTime=1553056487
&<Common request parameters>
```

#### Output sample code

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
                "ResourceTypeCn": "CloudAudit",
                "EventNameCn": "Search for logs"
            }
        ],
        "NextToken": "DnF1ZXJ5VGhlbkZldGNoDwAAAAAAACBuFjNoRHJ5YTd4U1B5YWY4c1ZmMmxBQWcAAAAAAAAgnBZZZkZoYy04LVJJeVpJNnZJS2hIVTdRAAAAAAAAI1QWYk5mQmZXTzhTWXFNZjFMVlhHY1RjdwAAAAAAAB9sFmhZbV8xbm1FUXE2NGVDQndWSlNoMncAAAAAAAAd9BZOelN1aGMycFNydUVEQ0dQbzdCcEZBAAAAAAAALroWMTh4c00xalhRbk9wR0NsYWZvV20tQQAAAAAAACCdFllmRmhjLTgtUkl5Wkk2dklLaEhVN1EAAAAAAAAuuRYxOHhzTTFqWFFuT3BHQ2xhZm9XbS1BAAAAAAAAIJ4WWWZGaGMtOC1SSXlaSTZ2SUtoSFU3UQAAAAAAAB81FnN5aTBfTWJKU25HdXZuMWxsRkdJZ3cAAAAAAAApMhZ1UjdybjlCY1NRYUZVYWRub2x4YW9RAAAAAAAAHzQWc3lpMF9NYkpTbkd1dm4xbGxGR0lndwAAAAAAAB31Fk56U3VoYzJwU3J1RURDR1BvN0JwRkEAAAAAAAAfbRZoWW1fMW5tRVFxNjRlQ0J3VkpTaDJ3AAAAAAAAH24WaFltXzFubUVRcTY0ZUNCd1ZKU2gydw==",
        "ListOver": true,
        "RequestId": "91e2998d-edc0-4ba0-a76d-cebbbfd99391"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=LookUpEvents)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, please see [Common Error Codes](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.SearchError | Internal error. Please submit a ticket. |
| InvalidParameter.Time | The parameter must contain the start time and end time and must be an integer timestamp (accurate to the second). |
| InvalidParameterValue.MaxResult | The maximum number of entries returned by one search is 50. |
| InvalidParameterValue.Time | The start time cannot be later than the end time. |
| InvalidParameterValue.attributeKey | Valid values of AttributeKey: RequestId, EventName, ReadOnly, Username, ResourceType, ResourceName, AccessKeyId. |
| LimitExceeded.OverTime | Only entries in the last 7 days can be searched for. |
