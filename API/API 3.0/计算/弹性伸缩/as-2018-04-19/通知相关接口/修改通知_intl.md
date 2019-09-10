## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (ModifyNotificationConfiguration) is used to modify notifications.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyNotificationConfiguration |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingNotificationId | Yes | String | ID of the notification to be modified. |
| NotificationTypes.N | No | Array of String | Notification type, i.e., the set of types of notifications to be subscribed to. Value range: <br/><li>SCALE_OUT_SUCCESSFUL: scale-out succeeded </li><li>SCALE_OUT_FAILED: scale-out failed </li><li>SCALE_IN_SUCCESSFUL: scale-in succeeded </li><li>SCALE_IN_FAILED: scale-in failed </li><li>REPLACE_UNHEALTHY_INSTANCE_SUCCESSFUL: unhealthy instance replacement succeeded </li><li>REPLACE_UNHEALTHY_INSTANCE_FAILED: unhealthy instance replacement failed </li> |
| NotificationUserGroupIds.N | No | Array of String | Notification group ID, which is the set of user group IDs and can be queried through the [DescribeUserGroup API](https://cloud.tencent.com/document/api/378/4404). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Modifying an Event Notification

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyNotificationConfiguration
&AutoScalingNotificationId=asn-2sestqbr
&NotificationTypes.0=SCALE_IN_SUCCESSFUL
&NotificationTypes.1=SCALE_IN_FAILED
&NotificationUserGroupIds.0=1678
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "52e32a5b-5f69-4d48-a3f1-f2fea5c43a70"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyNotificationConfiguration)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameterValue.UserGroupIdNotFound | The user group does not exist. |
| ResourceNotFound.AutoScalingNotificationNotFound | The notification does not exist. |
