## 1. API Description

API domain name: redis.tencentcloudapi.com.

Query the security group information of an instance

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeInstanceSecurityGroup |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | Yes | Array of String | Instance list |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceSecurityGroupsDetail | Array of [InstanceSecurityGroupDetail](/document/api/239/20022#InstanceSecurityGroupDetail) | Security group information of the instance |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying the Security Group Information of an Instance

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceSecurityGroup
&InstanceIds.0=crs-f2ho5rsz
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceSecurityGroupsDetail": [
      {
        "InstanceId": "crs-f2ho5rsz",
        "SecurityGroupDetails": [
          {
            "CreateTime": "2018-01-30 15:58:00",
            "InboundRule": [
              {
                "Action": "ACCEPT",
                "Ip": "0.0.0.0/0",
                "Port": "ALL",
                "Proto": "ALL"
              },
              {
                "Action": "ACCEPT",
                "Ip": "0.0.0.0/0",
                "Port": "ALL",
                "Proto": "ALL"
              }
            ],
            "OutboundRule": [
              {
                "Action": "ACCEPT",
                "Ip": "0.0.0.0/0",
                "Port": "ALL",
                "Proto": "ALL"
              }
            ],
            "ProjectId": 0,
            "SecurityGroupId": "sg-gl1egaj1",
            "SecurityGroupName": "all",
            "SecurityGroupRemark": ""
          }
        ]
      }
    ],
    "RequestId": "e546784b-709c-401d-aba6-73037eb4e522"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**


* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceSecurityGroup)

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
| InternalError.DbOperationFailed | Internal database operation (e.g., update, insert, or select) errors. |
| InternalError.InternalError | Internal error. |
| InvalidParameter | Parameter error |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| UnauthorizedOperation | Unauthorized operation. |
| UnauthorizedOperation.NoCAMAuthed | The operation performed is not authorized by CAM. |
| UnauthorizedOperation.UserNotInWhiteList | The user is not on the whitelist. |
