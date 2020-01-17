## 1. API Description

API request domain name: batch.tencentcloudapi.com.

This API is used to query task template information

Default API request frequency limit: 2 times/second.


## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/30473).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTaskTemplates |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/30473#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| TaskTemplateIds.N | No | Array of String | Task template ID |
| Filters.N | No | Array of [Filter](/document/api/599/30482#Filter) | Filter |
| Offset | No | Integer | Offset |
| Limit | No | Integer | Number of entries returned |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TaskTemplateSet | Array of [TaskTemplateView](/document/api/599/30482#TaskTemplateView) | Task template list |
| TotalCount | Integer | Number of task templates |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Querying a Task Template

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeTaskTemplates
&TaskTemplateIds.0=task-tmpl-pq24rq1e
&TaskTemplateIds.1=task-tmpl-606i415o
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "RequestId": "23f7d202-1cd4-4658-a989-88ad4ed77aac",
    "TaskTemplateSet": [
      {
        "CreateTime": "2018-03-08T03:27:43Z",
        "TaskTemplateDescription": "3ds Max 2018 Demo",
        "TaskTemplateId": "task-tmpl-pq24rq1e",
        "TaskTemplateInfo": {
          "Application": {
            "Command": "3dsmaxcmd Demo.max -outputName:c:\\\\render\\\\image.jpg",
            "DeliveryForm": "PACKAGE",
            "PackagePath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz"
          },
          "ComputeEnv": {
            "EnvData": {
              "DataDisks": [
                {
                  "DiskSize": "0",
                  "DiskType": "CLOUD_BASIC"
                }
              ],
              "ImageId": "img-i64lx84h",
              "InstanceType": "S1.LARGE8",
              "InternetAccessible": {
                "InternetChargeType": "TRAFFIC_POSTPAID_BY_HOUR",
                "InternetMaxBandwidthOut": "10"
              },
              "LoginSettings": {
                "Password": "B1habcdB1habcd"
              },
              "SystemDisk": {
                "DiskSize": "50",
                "DiskType": "CLOUD_BASIC"
              }
            },
            "EnvType": "MANAGED"
          },
          "FailedAction": "TERMINATE",
          "MaxRetryCount": 0,
          "OutputMappings": [
            {
              "DestinationPath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/",
              "SourcePath": "C:\\\\render\\\\"
            }
          ],
          "RedirectInfo": {
            "StderrRedirectPath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/wonderflet/logs/",
            "StdoutRedirectPath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/wonderflet/logs/"
          },
          "TaskInstanceNum": 1,
          "TaskName": "rendering",
          "Timeout": 259200
        },
        "TaskTemplateName": "rendering"
      },
      {
        "CreateTime": "2018-01-25T07:46:12Z",
        "TaskTemplateDescription": "",
        "TaskTemplateId": "task-tmpl-606i415o",
        "TaskTemplateInfo": {
          "Application": {
            "Command": "python -c \"fib=lambda n:1 if n&lt=2 else fib(n-1)+fib(n-2); print(fib(20))\" ",
            "DeliveryForm": "LOCAL"
          },
          "Authentications": [
            {
              "Scene": "COS",
              "SecretId": "AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
              "SecretKey": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
            }
          ],
          "ComputeEnv": {
            "EnvData": {
              "ImageId": "img-bq1gnde2",
              "InstanceType": "S1.SMALL1"
            },
            "EnvType": "MANAGED"
          },
          "FailedAction": "TERMINATE",
          "MaxRetryCount": 0,
          "RedirectInfo": {
            "StderrRedirectPath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/hello2/logs/",
            "StdoutRedirectPath": "cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/hello2/logs/"
          },
          "TaskInstanceNum": 2,
          "TaskName": "A"
        },
        "TaskTemplateName": "A"
      }
    ],
    "TotalCount": 2
  }
}
```

## 5. Developer Resources

**It is recommended to use [`API 3.0 Explorer`](https://console.cloud.tencent.com/api/explorer). This tool provides various capabilities such as online debugging, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

Cloud API 3.0 comes with a set of complementary development tools that make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/599/30479#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.TaskTemplateIdMalformed | Invalid task template ID format. |
| InvalidParameterValue | Invalid parameter value. |
| UnknownParameter | Unknown parameter error |

