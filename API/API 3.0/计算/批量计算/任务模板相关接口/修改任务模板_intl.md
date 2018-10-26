## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to modify a task template

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ModifyTaskTemplate |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| TaskTemplateId | Yes | String | Task template ID |
| TaskTemplateName | No | String | Task template Name |
| TaskTemplateDescription | No | String | Task template description |
| TaskTemplateInfo | No | [Task](/document/api/599/15912#Task) | Task template information |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Modifying a Task Template

#### Input

```
https://batch.tencentcloudapi.com/?Action=ModifyTaskTemplate
&TaskTemplateId=task-tmpl-606i415o
&TaskTemplateName=A
&TaskTemplateDescription=test
&TaskTemplateInfo.TaskName=A
&TaskTemplateInfo.TaskInstanceNum=1
&TaskTemplateInfo.Application.DeliveryForm=LOCAL
&TaskTemplateInfo.Application.Command=python -c "fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))"
&TaskTemplateInfo.ComputeEnv.EnvType=MANAGED
&TaskTemplateInfo.ComputeEnv.EnvData.InstanceType=S1.SMALL1
&TaskTemplateInfo.ComputeEnv.EnvData.ImageId=img-bd78fy2t
&TaskTemplateInfo.RedirectInfo.StdoutRedirectPath=cos://bucket-appid.cos.ap-guangzhou.myqcloud.com/hello2/logs/
&TaskTemplateInfo.RedirectInfo.StderrRedirectPath=cos://bucket-appid.ap-guangzhou.myqcloud.com/hello2/logs/
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "RequestId": "8a56bd93-688e-41c3-bc8b-f9867ffb0dd0"
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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| AllowedOneAttributeInEnvIdAndComputeEnv | One (and only one) parameter must be specified for ComputeEnv and EnvId. |
| InternalError | Internal error |
| InvalidParameter.CvmParameters | Invalid CVM parameter. |
| InvalidParameter.TaskName | Invalid task name. |
| InvalidParameter.TaskNameTooLong | The task name is too long. |
| InvalidParameter.TaskTemplateDescriptionTooLong | The task template description is too long. |
| InvalidParameter.TaskTemplateIdMalformed | Invalid task template ID format. |
| InvalidParameter.TaskTemplateName | Invalid task template name. |
| InvalidParameter.TaskTemplateNameTooLong | The task template name is too long. |
| InvalidParameterAtLeastOneAttribute | At least one of TaskTemplateName, TaskTemplateDescription and TaskTemplateInfo must be contained. |
| InvalidParameterValue.ComputeEnv | Compute environment parameter validation failed. |
| InvalidParameterValue.DependenceNotFoundTaskName | The dependent task definition could not be found. |
| InvalidParameterValue.DependenceUnfeasible | Loop task dependency is prohibited. |
| InvalidParameterValue.LocalPath | Invalid local storage path. |
| InvalidParameterValue.MaxRetryCount | The number of retries is too large. |
| InvalidParameterValue.Negative | Invalid negative parameter. |
| InvalidParameterValue.RemoteStoragePath | Invalid storage path format. |
| InvalidParameterValue.RemoteStorageSchemeType | Invalid storage type. |
| ResourceNotFound.TaskTemplate | The specified task template ID does not exist. |

