## 1. API Description

Domain name for API request: vpc.tencentcloudapi.com.

This API (CreateAddressTemplateGroup) is used to create an IP address template group.

A maximum of 100 requests can be initiated per second for this API.

Note: This API supports Finance regions. Since Finance regions and non-Finance regions are isolated and not interconnected. If the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region that should be identical to the value of Region field, for example: vpc.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/215/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateAddressTemplateGroup |
| Version | Yes |  String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes |  String | Common parameter. For more information, please see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/215/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AddressTemplateGroupName | Yes | String | IP address template group name. |
| AddressTemplateIds.N | Yes | Array of String | IP address template instance ID, such as ipm-mdunqeb6. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AddressTemplateGroup | [AddressTemplateGroup](https://cloud.tencent.com/document/api/215/##AddressTemplateGroup) | IP address template group object. |
| RequestId | String | The unique request ID, which is returned for each request. RequestId is required for locating a problem. |

## 4. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/215/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameterValue.Malformed | Invalid input parameter format. |
| ResourceNotFound | Resource does not exist. |

## 5. Example

### Example 1 Create an IP address template group

#### Input example

```
https://vpc.tencentcloudapi.com/?Action=CreateAddressTemplateGroup
&Version=2017-03-12
&AddressTemplateGroupName=TestName
&AddressTemplateIds.0=ipm-88t6207k
&AddressTemplateIds.1=ipm-mdunqeb6
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AddressTemplateGroup": {
      "AddressTemplateGroupId": "ipmg-dih8xdbq",
      "AddressTemplateGroupName": "TestName",
      "AddressTemplateIdSet": [
        "ipm-88t6207k",
        "ipm-mdunqeb6"
      ],
      "CreatedTime": "2018-04-03 21:51:02"
    },
    "RequestId": "20569756-56ba-4a13-b545-e1528d5cb239"
  }
}
```


## 6. Other Resources

Cloud API 3.0 comes with the following development tools to make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

