## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribePaiInstances) is used to query the information of PAI instances.

* You can query the detailed information of PAI instances based on information such as instance ID and instance domain name. For more information on filters, see `Filter`.
* If the parameter is null, a certain number of PAI instances (specified by `Limit` and 20 by default) of the current user is returned.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribePaiInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | No | Array of String | Queries by PAI instance ID. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. |
| Limit | No | Integer | Number of results to be returned. Default is 20. Maximum is 100. |
| Offset | No | Integer | Offset. It defaults to 0. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible PAI instances |
| PaiInstanceSet | Array of [PaiInstance](/document/api/377/20453#PaiInstance) | PAI instance details |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying PAI Instances

Query by PAI instance ID

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribePaiInstances
&InstanceIds.0=ins-6he2sztp
&InnstanceIds.1=ins-0xdrree5
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 2,
    "PaiInstanceSet": [
      {
        "InstanceId": "ins-6he2sztp",
        "BindingIp": "49.51.8.175",
        "DomainNameStatus": "ENABLED",
        "DomainName": "plumcot-j99466wb.pai.tcloudbase.com"
      },
      {
        "InstanceId": "ins-0xdrree5",
        "BindingIp": "45.113.71.202",
        "DomainNameStatus": "ENABLED",
        "DomainName": "berry-kotucbu9.pai.tcloudbase.com"
      }
    ],
    "RequestId": "61a4c56f-c216-42f0-8238-eeabe338633e"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribePaiInstances)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
