## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API returns user profile attributes such as gender, age, region and favorite celebrities, movies and TV shows through analysis of the insights into users interacting with brands (such as publicly commenting brand news or posting opinion on brands in social media).

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeUserPortrait |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Age | [AgePortraitInfo](/document/api/853/18402#AgePortraitInfo) | Age profile |
| Gender | [GenderPortraitInfo](/document/api/853/18402#GenderPortraitInfo) | Gender profile |
| Province | [ProvincePortraitInfo](/document/api/853/18402#ProvincePortraitInfo) | Province profile |
| Movie | [MoviePortraitInfo](/document/api/853/18402#MoviePortraitInfo) | Movie preference profile |
| Star | [StarPortraitInfo](/document/api/853/18402#StarPortraitInfo) | Favorite celebrity profile |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing User Profiles of a Brand

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeUserPortrait
&BrandId=qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujw%3D%3D
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Age": {
      "PortraitSet": [
        {
          "AgeRange": "0~18",
          "Percent": 10.98
        },
        {
          "AgeRange": "19~29",
          "Percent": 50.77
        },
        {
          "AgeRange": "30~39",
          "Percent": 28.42
        },
        {
          "AgeRange": "40~49",
          "Percent": 7.1
        },
        {
          "AgeRange": "50~69",
          "Percent": 2.45
        },
        {
          "AgeRange": "70+",
          "Percent": 0.28
        }
      ]
    },
    "Gender": {
      "PortraitSet": [
        {
          "Gender": "male",
          "Percent": 60
        },
        {
          "Gender": "female",
          "Percent": 40
        }
      ]
    },
    "Movie": {
      "PortraitSet": [
        {
          "Name": "With You",
          "Percent": 2.77
        },
        {
          "Name": "Happy Camp",
          "Percent": 2.42
        },
        {
          "Name": "My Amazing Boyfriend",
          "Percent": 2.51
        }
      ]
    },
    "Province": {
      "PortraitSet": [
        {
          "Percent": 0.93,
          "Province": "Tianjin"
        },
        {
          "Percent": 1.6,
          "Province": "Shanxi"
        },
        {
          "Percent": 12.86,
          "Province": "Fujian"
        },
        {
          "Percent": 1.47,
          "Province": "Gansu"
        },
        {
          "Percent": 0.17,
          "Province": "Qinghai"
        },
        {
          "Percent": 3.75,
          "Province": "Beijing"
        },
        {
          "Percent": 3.08,
          "Province": "Zhejiang"
        },
        {
          "Percent": 11.12,
          "Province": "Guangdong"
        },
        {
          "Percent": 1.47,
          "Province": "Heilongjiang"
        },
        {
          "Percent": 8.44,
          "Province": "Sichuan"
        },
        {
          "Percent": 2.14,
          "Province": "Anhui"
        },
        {
          "Percent": 1.34,
          "Province": "Xinjiang"
        },
        {
          "Percent": 5.09,
          "Province": "Henan"
        },
        {
          "Percent": 2.68,
          "Province": "Shanghai"
        },
        {
          "Percent": 2.81,
          "Province": "Hunan"
        },
        {
          "Percent": 0.53,
          "Province": "Guizhou"
        },
        {
          "Percent": 0.13,
          "Province": "Macao"
        },
        {
          "Percent": 0.8,
          "Province": "Jilin"
        },
        {
          "Percent": 0.53,
          "Province": "Ningxia"
        },
        {
          "Percent": 2.68,
          "Province": "Shaanxi"
        },
        {
          "Percent": 7.23,
          "Province": "Chongqing"
        },
        {
          "Percent": 1.6,
          "Province": "Jiangxi"
        },
        {
          "Percent": 0.26,
          "Province": "Taiwan"
        },
        {
          "Percent": 0.26,
          "Province": "Hong Kong"
        },
        {
          "Percent": 0.53,
          "Province": "Hainan"
        },
        {
          "Percent": 2.27,
          "Province": "Liaoning"
        },
        {
          "Percent": 0.93,
          "Province": "Inner Mongolia"
        },
        {
          "Percent": 3.61,
          "Province": "Hebei"
        },
        {
          "Percent": 0,
          "Province": "Tibet"
        },
        {
          "Percent": 2.81,
          "Province": "Hubei"
        },
        {
          "Percent": 6.97,
          "Province": "Shandong"
        },
        {
          "Percent": 6.56,
          "Province": "Jiangsu"
        },
        {
          "Percent": 1.34,
          "Province": "Yunnan"
        },
        {
          "Percent": 2.01,
          "Province": "Guangxi"
        }
      ]
    },
    "RequestId": "53240088-ccd6-4e4a-a7c5-c5a256806894",
    "Star": {
      "PortraitSet": [
        {
          "Name": "Lam Ching Ying",
          "Percent": 2.77
        },
        {
          "Name": "Gloria Tang Tsz-kei",
          "Percent": 2.42
        },
        {
          "Name": "Jackie Chan",
          "Percent": 2.51
        }
      ]
    }
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeUserPortrait)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API are listed below. For other error codes, see [Common Error Codes](/document/api/853/18389#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DataInProcessing | Processing data. |
| InternalError.MetaDataOpFailed | Metadata operation failed. |
| InvalidParameter | Parameter error |
| ResourceNotFound | Resource does not exist |
| UnauthorizedOperation | Unauthorized operation |

