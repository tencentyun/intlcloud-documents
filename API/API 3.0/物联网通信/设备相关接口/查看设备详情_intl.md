## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (DescribeDevice) is used to view device information.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeDevice |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| ProductID | Yes | String | Product ID |
| DeviceName | Yes | String | Device name |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DeviceName | String | Device name |
| Online | Integer | Whether the device online; 0 - offline; 1 - online |
| LoginTime | Integer | Login time of the device |
| Version | String | Firmware version of the device |
| LastUpdateTime | Integer | Last update time of the device |
| DeviceCert | String | Device certificate |
| DevicePsk | String | Device key |
| Tags | Array of [DeviceTag](/document/api/634/19497#DeviceTag) | Device attributes |
| DeviceType | Integer | Device type |
| Imei | String | IMEI |
| Isp | Integer | ISP type |
| ConnIP | Integer | IP address |
| NbiotDeviceID | String | DeviceID at the NB IoT ISP |
| LoraDevEui | String | DevEui of a LoRa device |
| LoraMoteType | Integer | MoteType of a LoRa device |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Device Details

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=DescribeDevice
&ProductID=ABCDE12345
&DeviceName=abc
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "DeviceName": "",
    "ConnIP": 0,
    "DevicePsk": "",
    "LastUpdateTime": 0,
    "Tags": [
      {
        "Tag": "category",
        "Type": 2,
        "Value": ""
      },
      {
        "Tag": "note",
        "Type": 2,
        "Value": ""
      }
    ],
    "Isp": 0,
    "LoraMoteType": 0,
    "NbiotDeviceID": "",
    "LoraDevEui": "",
    "Version": "",
    "DeviceType": 3,
    "RequestId": "be69a7a3-7315-40a7-9532-3316e4a3e97e",
    "DeviceCert": "-----BEGIN CERTIFICATE-----\nIIDS...Fw==\n-----END CERTIFICATE-----\n",
    "Online": 0,
    "Imei": "",
    "LoginTime": 0
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=DescribeDevice)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/634/19474#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| ResourceNotFound.DeviceNotExist | Device does not exist. |
| ResourceNotFound.ProductNotExist | Product does not exist. |
