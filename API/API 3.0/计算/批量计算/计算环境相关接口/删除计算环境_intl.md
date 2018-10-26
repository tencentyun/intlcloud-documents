## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is　ｕsed to delete a compute environment.

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DeleteComputeEnv |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| EnvId | Yes | String | Compute environment ID |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Deleting a Compute Environment

#### Input 

```
https://batch.tencentcloudapi.com/?Action=DeleteComputeEnv
&EnvId=env-3dhmblr3
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "RequestId": "8b71050a-55c1-4f3b-bf66-5e4f8510a5a0"
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

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.EnvIdMalformed | Invalid compute environment ID format. |
| ResourceNotFound.ComputeEnv | The specified compute environment does not exist. |
| UnsupportedOperation.AcceptOtherRequest | Another request is being processed and deletion is prohibited. |
| UnsupportedOperation.ComputeEnvOperation | Deletion is prohibited. |
| UnsupportedOperation.ComputeNodeForbidTerminate | It is prohibited to terminate the compute node. |

