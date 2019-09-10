## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeLaunchConfigurations) is used to query the information of a launch configuration.

* You can query the launch configuration details based on information such as launch configuration ID and name. For more information on filters, see `Filter`.
* If the parameter is empty, a number (same as the `Limit`. The default is 20) of launch configurations will be returned.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeLaunchConfigurations |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LaunchConfigurationIds.N | No | Array of String | Query by one or more launch configuration IDs in the format of `asc-ouy1ax38`. The maximum quantity per request is 100. This parameter does not support specifying both `LaunchConfigurationIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter conditions. <br/><li> launch-configuration-id - String - Required: No - (Filter condition) Filter by launch configuration ID. </li><li> launch-configuration-name - String - Required: No - (Filter condition) Filter by launch configuration name. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `LaunchConfigurationIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of launch configurations that meet the condition |
| LaunchConfigurationSet | Array of [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration) | List of launch configuration details |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Using Filters to View the Launch Configuration List

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&Filters.0.Name=launch-configuration-id
&Filters.0.Values.0=asc-l7rduvv0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "LaunchConfigurationSet": [
      {
        "ProjectId": 0,
        "LaunchConfigurationId": "asc-l7rduvv0",
        "VersionNumber": 1,
        "LaunchConfigurationName": "lc2",
        "AutoScalingGroupAbstractSet": [],
        "InstanceType": "S2.SMALL2",
        "InstanceTypes": [
          "S2.SMALL2"
        ],
        "InstanceChargeType": "POSTPAID_BY_HOUR",
        "InstanceMarketOptions": null,
        "SystemDisk": {
          "DiskType": "LOCAL_BASIC",
          "DiskSize": 50
        },
        "DataDisks": [
          {
            "DiskType": "LOCAL_BASIC",
            "DiskSize": 50
          }
        ],
        "LoginSettings": {
          "KeyIds": []
        },
        "InternetAccessible": {
          "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 1,
          "PublicIpAssigned": true
        },
        "SecurityGroupIds": [],
        "EnhancedService": {
          "SecurityService": {
            "Enabled": true
          },
          "MonitorService": {
            "Enabled": true
          }
        },
        "UserData": null,
        "CreatedTime": "2018-05-03T03:23:10Z",
        "UpdatedTime": "2018-05-03T03:23:10Z"
      }
    ],
    "RequestId": "15f9582f-72ff-4b5f-91b6-ff905782391b"
  }
}
```

### Sample 2. Querying Launch Configuration List by Launch Configuration ID

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&LaunchConfigurationIds.0=asc-l7rduvv0
&LaunchConfigurationIds.1=asc-2ejax3t8
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 2,
    "LaunchConfigurationSet": [
      {
        "ProjectId": 0,
        "LaunchConfigurationId": "asc-2ejax3t8",
        "VersionNumber": 1,
        "LaunchConfigurationName": "lc1",
        "AutoScalingGroupAbstractSet": [],
        "InstanceType": "D1.2XLARGE32",
        "InstanceTypes": [
          "D1.2XLARGE32"
        ],
        "InstanceChargeType": "POSTPAID_BY_HOUR",
        "InstanceMarketOptions": null,
        "SystemDisk": {
          "DiskType": "LOCAL_BASIC",
          "DiskSize": 50
        },
        "DataDisks": [],
        "LoginSettings": {
          "KeyIds": []
        },
        "InternetAccessible": {
          "InternetChargeType": "TRAFFIC_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 0,
          "PublicIpAssigned": false
        },
        "SecurityGroupIds": [],
        "EnhancedService": {
          "SecurityService": {
            "Enabled": true
          },
          "MonitorService": {
            "Enabled": true
          }
        },
        "UserData": null,
        "CreatedTime": "2018-05-03T06:37:48Z",
        "UpdatedTime": "2018-05-03T06:37:48Z"
      },
      {
        "ProjectId": 0,
        "LaunchConfigurationId": "asc-l7rduvv0",
        "VersionNumber": 1,
        "LaunchConfigurationName": "lc2",
        "AutoScalingGroupAbstractSet": [],
        "InstanceType": "S2.SMALL2",
        "InstanceTypes": [
          "S2.SMALL2"
        ],
        "InstanceChargeType": "POSTPAID_BY_HOUR",
        "InstanceMarketOptions": null,
        "SystemDisk": {
          "DiskType": "LOCAL_BASIC",
          "DiskSize": 50
        },
        "DataDisks": [
          {
            "DiskType": "LOCAL_BASIC",
            "DiskSize": 50
          }
        ],
        "LoginSettings": {
          "KeyIds": []
        },
        "InternetAccessible": {
          "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 1,
          "PublicIpAssigned": true
        },
        "SecurityGroupIds": [],
        "EnhancedService": {
          "SecurityService": {
            "Enabled": true
          },
          "MonitorService": {
            "Enabled": true
          }
        },
        "UserData": null,
        "CreatedTime": "2018-05-03T03:23:10Z",
        "UpdatedTime": "2018-05-03T03:23:10Z"
      }
    ],
    "RequestId": "f7dd68bc-d5e3-4a43-92a5-bde6d8fe9bd4"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeLaunchConfigurations)

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
| InvalidFilter | Invalid filter. |
| InvalidLaunchConfiguration | Invalid launch configuration |
| InvalidLaunchConfigurationId | Invalid launch configuration ID |
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidPermission | The account does not support this operation. |
