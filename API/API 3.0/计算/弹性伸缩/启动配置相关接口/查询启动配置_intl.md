## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (DescribeLaunchConfigurations) is used to query the information of one or more launch configurations.

Default request rate limit: 10/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeLaunchConfigurations |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LaunchConfigurationIds.N | No | Array of String | ID(s) of the launch configuration(s) to be queried, such as `asc-ouy1ax38`. A maximum of 100 launch configurations can be queried at one time. You cannot specify both `LaunchConfigurationIds` and `Filters`. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. <br/><li> `launch-configuration-id` - String - Required: No - (Filter condition) Filter by launch configuration ID. </li><li> `launch-configuration-name` - String - Required: No - (Filter condition) Filter by launch configuration name. </li><br/> You can specify 10 `Filters` and 5 `Filter.Values` in one request. You cannot specify both `LaunchConfigurationIds` and `Filters`. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. It is 0 by default. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of launch configurations that meet the condition |
| LaunchConfigurationSet | Array of [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration) | List of launch configuration details |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the list of launch configurations using Filters

#### Input example

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&Filters.0.Name=launch-configuration-id
&Filters.0.Values.0=asc-l7rduvv0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "LaunchConfigurationSet": [
      {
        "AutoScalingGroupAbstractSet": [],
        "CreatedTime": "2018-05-03T03:23:10Z",
        "DataDisks": [
          {
            "DiskSize": 50,
            "DiskType": "LOCAL_BASIC"
          }
        ],
        "EnhancedService": {
          "MonitorService": {
            "Enabled": true
          },
          "SecurityService": {
            "Enabled": true
          }
        },
        "InstanceType": "S2.SMALL2",
        "InternetAccessible": {
          "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 1,
          "PublicIpAssigned": true
        },
        "LaunchConfigurationId": "asc-l7rduvv0",
        "LaunchConfigurationName": "lc2",
        "LoginSettings": {
          "KeyIds": []
        },
        "ProjectId": 0,
        "SecurityGroupIds": [],
        "SystemDisk": {
          "DiskSize": 50,
          "DiskType": "LOCAL_BASIC"
        },
        "UserData": null
      }
    ],
    "RequestId": "15f9582f-72ff-4b5f-91b6-ff905782391b",
    "TotalCount": 1
  }
}
```

### Example 2 Query the list of launch configurations using launch configuration ID

#### Input example

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&LaunchConfigurationIds.0=asc-l7rduvv0
&LaunchConfigurationIds.1=asc-2ejax3t8
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "LaunchConfigurationSet": [
      {
        "AutoScalingGroupAbstractSet": [],
        "CreatedTime": "2018-05-03T06:37:48Z",
        "DataDisks": [],
        "EnhancedService": {
          "MonitorService": {
            "Enabled": true
          },
          "SecurityService": {
            "Enabled": true
          }
        },
        "InstanceType": "D1.2XLARGE32",
        "InternetAccessible": {
          "InternetChargeType": "TRAFFIC_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 0,
          "PublicIpAssigned": false
        },
        "LaunchConfigurationId": "asc-2ejax3t8",
        "LaunchConfigurationName": "lc1",
        "LoginSettings": {
          "KeyIds": []
        },
        "ProjectId": 0,
        "SecurityGroupIds": [],
        "SystemDisk": {
          "DiskSize": 50,
          "DiskType": "LOCAL_BASIC"
        },
        "UserData": null
      },
      {
        "AutoScalingGroupAbstractSet": [],
        "CreatedTime": "2018-05-03T03:23:10Z",
        "DataDisks": [
          {
            "DiskSize": 50,
            "DiskType": "LOCAL_BASIC"
          }
        ],
        "EnhancedService": {
          "MonitorService": {
            "Enabled": true
          },
          "SecurityService": {
            "Enabled": true
          }
        },
        "InstanceType": "S2.SMALL2",
        "InternetAccessible": {
          "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
          "InternetMaxBandwidthOut": 1,
          "PublicIpAssigned": true
        },
        "LaunchConfigurationId": "asc-l7rduvv0",
        "LaunchConfigurationName": "lc2",
        "LoginSettings": {
          "KeyIds": []
        },
        "ProjectId": 0,
        "SecurityGroupIds": [],
        "SystemDisk": {
          "DiskSize": 50,
          "DiskType": "LOCAL_BASIC"
        },
        "UserData": null
      }
    ],
    "RequestId": "f7dd68bc-d5e3-4a43-92a5-bde6d8fe9bd4",
    "TotalCount": 2
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeLaunchConfigurations)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidFilter | Invalid filter |
| InvalidLaunchConfiguration | Invalid launch configuration |
| InvalidLaunchConfigurationId | Invalid launch configuration ID |
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidPermission | This operation is not supported for the account |

