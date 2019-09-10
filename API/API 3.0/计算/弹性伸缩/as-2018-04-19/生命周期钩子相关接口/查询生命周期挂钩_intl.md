## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeLifecycleHooks) is used to query the information of lifecycle hooks.

* You can query the details of lifecycle hooks based on information such as auto scaling group ID, lifecycle hook ID, or lifecycle hook name. For more information on filters, see `Filter`.
* If the parameter is empty, a certain number of lifecycle hooks (specified by `Limit` and 20 by default) of the current user is returned.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeLifecycleHooks |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LifecycleHookIds.N | No | Array of String | Query by one or more lifecycle hook IDs in the format of `ash-8azjzxcl`. The maximum quantity per request is 100. This parameter does not support specifying both `LifecycleHookIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> lifecycle-hook-id - String - Required: No - (Filter) Filter by lifecycle hook ID. </li><li> lifecycle-hook-name - String - Required: No - (Filter) Filter by lifecycle hook name. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by auto scaling group ID. </li><br/>Filter. <br/><li> lifecycle-hook-id - String - Required: No - (Filter) Filter by lifecycle hook ID. </li><li> lifecycle-hook-name - String - Required: No - (Filter) Filter by lifecycle hook name. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by auto scaling group ID. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `LifecycleHookIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| LifecycleHookSet | Array of [LifecycleHook](/document/api/377/20453#LifecycleHook) | Array of lifecycle hooks |
| TotalCount | Integer | Total quantity |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying Lifecycle Hooks

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeLifecycleHooks
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 4,
    "LifecycleHookSet": [
      {
        "LifecycleHookName": "terminate-topic",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 120,
        "NotificationMetadata": "topic",
        "NotificationTarget": {
          "TargetType": "CMQ_TOPIC",
          "TopicName": "one-topic",
          "QueueName": ""
        },
        "CreatedTime": "2019-04-19T02:59:30Z",
        "DefaultResult": "ABANDON",
        "LifecycleHookId": "ash-oq76wsrx",
        "LifecycleTransition": "INSTANCE_TERMINATING"
      },
      {
        "LifecycleHookName": "launch-queue",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 120,
        "NotificationMetadata": "queue",
        "NotificationTarget": {
          "TargetType": "CMQ_QUEUE",
          "TopicName": "",
          "QueueName": "one-queue"
        },
        "CreatedTime": "2019-04-19T02:57:14Z",
        "DefaultResult": "CONTINUE",
        "LifecycleHookId": "ash-fbjiexz7",
        "LifecycleTransition": "INSTANCE_LAUNCHING"
      },
      {
        "LifecycleHookName": "one-hook",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 360,
        "NotificationMetadata": "",
        "NotificationTarget": {
          "TargetType": "",
          "TopicName": "",
          "QueueName": ""
        },
        "CreatedTime": "2019-04-19T02:56:02Z",
        "DefaultResult": "CONTINUE",
        "LifecycleHookId": "ash-heyubibl",
        "LifecycleTransition": "INSTANCE_LAUNCHING"
      },
      {
        "LifecycleHookName": "one-hook-default",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 300,
        "NotificationMetadata": "",
        "NotificationTarget": {
          "TargetType": "",
          "TopicName": "",
          "QueueName": ""
        },
        "CreatedTime": "2019-04-19T02:51:24Z",
        "DefaultResult": "CONTINUE",
        "LifecycleHookId": "ash-8azjzxj9",
        "LifecycleTransition": "INSTANCE_LAUNCHING"
      }
    ],
    "RequestId": "dff07f6e-bdbc-4532-baeb-e7fb3aebe248"
  }
}
```

### Sample 2. Query Lifecycle Hooks with a Filter

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeLifecycleHooks
&Filters.0.Name=lifecycle-hook-id
&Filters.0.Values.0=ash-oq76wsrx
&Filters.0.Values.1=ash-fbjiexz7
&Filters.1.Name=auto-scaling-group-id
&Filters.1.Values.0=asg-8fbozqja
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 2,
    "LifecycleHookSet": [
      {
        "LifecycleHookName": "terminate-topic",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 120,
        "NotificationMetadata": "topic",
        "NotificationTarget": {
          "TargetType": "CMQ_TOPIC",
          "TopicName": "one-topic",
          "QueueName": ""
        },
        "CreatedTime": "2019-04-19T02:59:30Z",
        "DefaultResult": "ABANDON",
        "LifecycleHookId": "ash-oq76wsrx",
        "LifecycleTransition": "INSTANCE_TERMINATING"
      },
      {
        "LifecycleHookName": "launch-queue",
        "AutoScalingGroupId": "asg-8fbozqja",
        "HeartbeatTimeout": 120,
        "NotificationMetadata": "queue",
        "NotificationTarget": {
          "TargetType": "CMQ_QUEUE",
          "TopicName": "",
          "QueueName": "one-queue"
        },
        "CreatedTime": "2019-04-19T02:57:14Z",
        "DefaultResult": "CONTINUE",
        "LifecycleHookId": "ash-fbjiexz7",
        "LifecycleTransition": "INSTANCE_LAUNCHING"
      }
    ],
    "RequestId": "2d774a6c-bcaa-4805-b0cd-bd64519e2538"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeLifecycleHooks)

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
| InvalidFilter | Invalid filter. |
| InvalidParameter | Incorrect parameter |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| MissingParameter | Missing parameter. |
