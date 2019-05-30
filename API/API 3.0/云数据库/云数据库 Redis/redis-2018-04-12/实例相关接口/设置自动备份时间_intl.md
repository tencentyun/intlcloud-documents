## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API schedules auto backup.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyAutoBackupConfig |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID |
| WeekDays.N | Yes | Array of String | Date; valid values: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday |
| TimePeriod | Yes | String | Time period; valid values: 00:00-01:00, 01:00-02:00...... 23:00-00:00 |
| AutoBackupType | No | Integer | Auto backup type: 1 "scheduled rollback" |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| AutoBackupType | Integer | Auto backup type: 1 "scheduled rollback" |
| WeekDays | Array of String | Date; valid values: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday. |
| TimePeriod | String | Time period; valid values: 00:00-01:00, 01:00-02:00...... 23:00-00:00 |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=ModifyAutoBackupConfig
&InstanceId=crs-5a4py64p
&TimePeriod=00%3A00-01%3A00
&AutoBackupType=1
&WeekDays.0=Wednesday
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoBackupType": 1,
    "WeekDays": [
      "Wednesday"
    ],
    "TimePeriod": "00:00-01:00",
    "RequestId": "ac750a85-9a55-4a42-a9de-8c2ca1f4ff12"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=ModifyAutoBackupConfig)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.Unknown | Invalid data is entered for weekday. |
| InternalError.InternalError | Internal error. |
| InvalidParameter.InvalidParameter | Business parameter error. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.WeekDaysIsInvalid | Invalid data is entered for weekday. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
