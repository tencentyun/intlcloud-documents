## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeLaunchConfigurations) is used to query the information of a launch configuration.

* You can query the launch configuration details based on information such as launch configuration ID and name. For more information about filters, see `Filter`.
* If the parameter is empty, a certain number of launch configurations (specified by `Limit` and 20 by default) of the current user is returned.

Default API request frequency limit: 10 times/second.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeLaunchConfigurations |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| LaunchConfigurationIds.N | No | Array of String | Query by one or more launch configuration IDs. Launch configuration ID example: `asc-ouy1ax38`. The upper limit per request is 100. The parameter does not support specifying both `LaunchConfigurationIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> launch-configuration-id - String - Required: No - (Filter) Filter by launch configuration ID. </li><li> launch-configuration-name - String - Required: No - (Filter) Filter by launch configuration name. </li><br/>The maximum number of `Filters` per request is 10. The upper limit for `Filter.Values` is 5. The parameter does not support specifying both `LaunchConfigurationIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about `Limit`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset, 0 by default. For more information about `Offset`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible launch configurations. |
| LaunchConfigurationSet | Array of [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration) | List of launch configuration details. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Using Filters to View the Launch Configuration List

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
                "CreatedTime": "2018-05-03T03:23:10Z"
            }
        ],
        "RequestId": "15f9582f-72ff-4b5f-91b6-ff905782391b"
    }
}
```

### Querying Launch Configuration List by Launch Configuration ID

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
                "CreatedTime": "2018-05-03T06:37:48Z"
            },
            {
                "ProjectId": 0,
                "LaunchConfigurationId": "asc-l7rduvv0",
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
                "CreatedTime": "2018-05-03T03:23:10Z"
            }
        ],
        "RequestId": "f7dd68bc-d5e3-4a43-92a5-bde6d8fe9bd4"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeLaunchConfigurations)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidFilter | Invalid filter. |
| InvalidLaunchConfiguration | Invalid launch configuration. |
| InvalidLaunchConfigurationId | The launch configuration ID is invalid. |
| InvalidParameterConflict | The two parameters specified conflict and cannot co-exist. |
| InvalidPermission | The account does not support this operation. |
