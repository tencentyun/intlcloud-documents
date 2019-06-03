## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API modifies instance-related information (currently supports renaming instances)

Default API request rate limit: 50 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyInstance |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Operation | Yes | String | Instance modification type. rename: rename the instance; modifyProject: modify the project of the instance; modifyAutoRenew: modify the auto-renewal flag of the instance |
| InstanceId | No | String | Instance ID |
| InstanceName | No | String | New name of the instance |
| ProjectId | No | Integer | Project ID |
| AutoRenew | No | Integer | Auto-renewal flag. 0: default status (manual renewal); 1: auto-renewal; 2: auto-renewal clearly banned |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=ModifyInstance
&Operation=rename&InstanceIds.0=crs-r3nqjq3n&InstanceNames.0=newname1&InstanceIds.1=crs-9bvd9b8v&InstanceNames.1=newname2
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "6d1e8909-496a-4f27-ad0d-2e4a069b52c0"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=ModifyInstance)

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
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| UnauthorizedOperation | Unauthorized operation. |
| UnauthorizedOperation.NoCAMAuthed | The operation performed is not authorized by CAM. |
| UnauthorizedOperation.UserNotInWhiteList | The user is not on the whitelist. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | The Redis cluster mode instance is not allowed to access a security group. |
| UnsupportedOperation.IsAutoRenewError | Error with the auto-renewal flag. |
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | Only cluster mode instances support backup exporting. |
