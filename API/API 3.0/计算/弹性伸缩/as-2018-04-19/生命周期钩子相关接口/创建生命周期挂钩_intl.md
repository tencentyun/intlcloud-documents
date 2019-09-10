## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CreateLifeCycleHook) is used to create new lifecycle hooks.

* You can configure message notifications in the following format for lifecycle hooks, which will be sent to your CMQ queue by AS:

```
{
	"Service": "Tencent Cloud Auto Scaling",
	"Time": "2019-03-14T10:15:11Z",
	"AppId": "1251783334",
	"ActivityId": "asa-fznnvrja",
	"AutoScalingGroupId": "asg-rrrrtttt",
	"LifecycleHookId": "ash-xxxxyyyy",
	"LifecycleHookName": "my-hook",
	"LifecycleActionToken": "3080e1c9-0efe-4dd7-ad3b-90cd6618298f",
	"InstanceId": "ins-aaaabbbb",
	"LifecycleTransition": "INSTANCE_LAUNCHING",
	"NotificationMetadata": ""
}
```

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateLifecycleHook |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| LifecycleHookName | Yes | String | Lifecycle hook name, which can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points with a maximum length of 128 bytes. |
| LifecycleTransition | Yes | String | Scenario for the lifecycle hook. Value range: INSTANCE_LAUNCHING, INSTANCE_TERMINATING |
| DefaultResult | No | String | Define the action to be taken by the auto scaling group upon lifecycle hook timeout. Value range: CONTINUE, ABANDON. Default value: CONTINUE |
| HeartbeatTimeout | No | Integer | The maximum length of time (in seconds) that can elapse before the lifecycle hook times out. Value range: 30-3,600. Default value: 300 |
| NotificationMetadata | No | String | Additional information sent by AS to the notification target. The default value is ''. The maximum length is 1,024 bytes |
| NotificationTarget | No | [NotificationTarget](/document/api/377/20453#NotificationTarget) | Notification target |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| LifecycleHookId | String | Lifecycle hook ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Creating a Lifecycle Hook with Default Values

Create a lifecycle hook that takes effect during instance creation, where DefaultResult takes the default value of CONTINUE and HeartbeatTimeout takes the default value of 300 seconds.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLifecycleHook
&AutoScalingGroupId=asg-8fbozqja
&LifecycleHookName=one-hook-default
&LifecycleTransition=INSTANCE_LAUNCHING
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "LifecycleHookId": "ash-8azjzxj9",
    "RequestId": "4fa9fd2e-5b6c-49fe-9ba7-ed2ee62d8271"
  }
}
```

### Sample 2. Creating a Lifecycle Hook

Create a lifecycle hook that takes effect during instance creation, where DefaultResult is set to ABANDON and HeartbeatTimeout is set to 360 seconds.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLifecycleHook
&AutoScalingGroupId=asg-8fbozqja
&DefaultResult=ABANDON
&HeartbeatTimeout=360
&LifecycleHookName=one-hook
&LifecycleTransition=INSTANCE_LAUNCHING
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "LifecycleHookId": "ash-heyubibl",
    "RequestId": "5e414011-3359-45bd-8ba4-5b503d3fd3f6"
  }
}
```

### Sample 3. Creating a Lifecycle Hook to Notify a CMQ Queuing Model

Create a lifecycle hook that takes effect during instance creation, where the DefaultResult is set to CONTINUE and the HeartbeatTimeout is set to 120 seconds to notify the CMQ queuing model named "one-queue".

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLifecycleHook
&AutoScalingGroupId=asg-8fbozqja
&DefaultResult=CONTINUE
&HeartbeatTimeout=120
&LifecycleHookName=launch-queue
&LifecycleTransition=INSTANCE_LAUNCHING
&NotificationMetadata=queue
&NotificationTarget.TargetType=CMQ_QUEUE
&NotificationTarget.QueueName=one-queue
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "LifecycleHookId": "ash-fbjiexz7",
    "RequestId": "d3cf27b7-3090-4317-9107-d2eac986a446"
  }
}
```

### Sample 4. Creating a Lifecycle Hook to Notify a CMQ Topic Model

Create a lifecycle hook that takes effect during instance termination, where the DefaultResult is set to ABANDON and the HeartbeatTimeout is set to 120 seconds to notify the CMQ topic model named "one-topic".

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLifecycleHook
&AutoScalingGroupId=asg-8fbozqja
&DefaultResult=ABANDON
&HeartbeatTimeout=120
&LifecycleHookName=terminate-topic
&LifecycleTransition=INSTANCE_TERMINATING
&NotificationMetadata=topic
&NotificationTarget.TargetType=CMQ_TOPIC
&NotificationTarget.TopicName=one-topic
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "LifecycleHookId": "ash-oq76wsrx",
    "RequestId": "cdb7670b-0412-444f-9d2f-0da9cd07c410"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateLifecycleHook)

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
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue | Invalid parameter value |
| InvalidParameterValue.Filter | Invalid filter |
| InvalidParameterValue.LifecycleHookNameDuplicated | The lifecycle hook name already exists. |
| MissingParameter | Missing parameter. |
