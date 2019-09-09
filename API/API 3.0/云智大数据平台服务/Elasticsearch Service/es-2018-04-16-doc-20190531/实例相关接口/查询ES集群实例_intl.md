## 1. API Description

API domain name: es.tencentcloudapi.com.

This API queries all instances eligible in the specified region for the specified user account.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter Region, we recommend you include that financial region in your domain name  , such as es.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/845/30623).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeInstances |
| Version | Yes | String | Common parameter. The version of this API: 2018-04-16 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | No | String | Availability Zone of the cluster instance. If no value is specified for this parameter, all Availability Zones are assigned. |
| InstanceIds.N | No | Array of String | List of cluster instance IDs |
| InstanceNames.N | No | Array of String | List of cluster instance names |
| Offset | No | Integer | Pagination start value; default value is 0 |
| Limit | No | Integer | Number of entries per page; default value is 20 |
| OrderByKey | No | Integer | Sort by field <li>1: Instance ID </li><li>2: Instance name </li><li>3: AZ </li><li>4: Creation time </li>If orderKey is not passed in, sort by creation time in descending order |
| OrderByType | No | Integer | Sorting order <li>0: Ascending </li><li>1: Descending </li>If orderByKey is passed in but orderByType is not, ascending order is used by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of returned instances |
| InstanceList | Array of [InstanceInfo](/document/api/845/30634#InstanceInfo) | List of instance details |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Querying ES Cluster Instances

Query the eligible ES cluster instances according to the given criteria and return their details

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=DescribeInstances
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 2,
    "InstanceList": [
      {
        "InstanceId": "es-sample",
        "InstanceName": "es-sample",
        "InstanceType": 2,
        "Region": "ap-guangzhou",
        "Zone": "ap-guangzhou-2",
        "AppId": 0,
        "Uin": "xxxxxxxx",
        "VpcUid": "vpc-sample",
        "SubnetUid": "subnet-sample",
        "Status": 1,
        "ChargeType": "PREPAID",
        "ChargePeriod": 1,
        "RenewFlag": "RENEW_FLAG_DEFAULT",
        "NodeType": "ES.S1.SMALL2",
        "NodeNum": 2,
        "CpuNum": 1,
        "MemSize": 2,
        "DiskType": "",
        "DiskSize": 100,
        "EsDomain": "es-sample.tencentelasticsearch.com",
        "EsVip": "0.0.0.0",
        "EsPort": 9200,
        "KibanaUrl": "https://es-sample.kibana.tencentelasticsearch.com:5601",
        "EsVersion": "5.6.4",
        "EsConfig": "{}",
        "EsAcl": {
          "WhiteIpList": [],
          "BlackIpList": []
        },
        "CreateTime": "2018-07-27 17:28:04",
        "UpdateTime": "2018-07-30 10:22:29",
        "Deadline": "2018-08-27 17:28:04"
      },
      {
        "InstanceId": "es-sample2",
        "InstanceName": "es-sample2",
        "InstanceType": 2,
        "Region": "ap-guangzhou",
        "Zone": "ap-guangzhou-4",
        "AppId": 0,
        "Uin": "xxxxxx",
        "VpcUid": "vpc-sample",
        "SubnetUid": "subnet-sample",
        "Status": 1,
        "ChargeType": "PREPAID",
        "ChargePeriod": 1,
        "RenewFlag": "RENEW_FLAG_DEFAULT",
        "NodeType": "ES.S1.MEDIUM4",
        "NodeNum": 2,
        "CpuNum": 2,
        "MemSize": 4,
        "DiskType": "",
        "DiskSize": 100,
        "EsDomain": "es-sample.tencentelasticsearch.com",
        "EsVip": "0.0.0.0",
        "EsPort": 9200,
        "KibanaUrl": "https://es-sample.kibana.tencentelasticsearch.com:5601",
        "EsVersion": "5.6.4",
        "EsConfig": "{}",
        "EsAcl": {
          "WhiteIpList": [],
          "BlackIpList": []
        },
        "CreateTime": "2018-07-26 17:47:47",
        "UpdateTime": "2018-07-26 18:16:50",
        "Deadline": "2018-08-26 17:47:47"
      }
    ],
    "RequestId": "5d5a201f-0a3d-485f-a82f-3c73ccca348a"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=DescribeInstances)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
