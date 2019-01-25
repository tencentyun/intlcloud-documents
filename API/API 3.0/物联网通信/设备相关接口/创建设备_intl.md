## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (CreateDevice) is used to create a new IoT Hub device.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateDevice |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| ProductId | Yes | String | Product ID. This is the globally unique ID of the product assigned to the user by Tencent Cloud upon product creation |
| DeviceName | Yes | String | Device name. Naming rule: [a-zA-Z0-9:_-]{1,48}. |
| Attribute | No | [Attribute](/document/api/634/19497#Attribute) | Device attributes |
| DefinedPsk | No | String | Whether to use a custom PSK; no by default |
| Isp | No | Integer | ISP type. This field is required when the product is an NB-IoT product. 1 - China Telecom; 2 - China Mobile; 3 - China Unicom |
| Imei | No| String | IMEI. This field is required when the product is an NB-IoT product |
| LoraDevEui | No | String | DevEui of a LoRa device. This field is required when creating a LoRa device |
| LoraMoteType | No | Integer | MoteType of a LoRa device |
| Skey | No | String | The skey required when creating a LoRa device |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DeviceName | String | Device name |
| DevicePsk | String | Symmetric encryption key encoded with Base64. This parameter will be returned if symmetric encryption is used |
| DeviceCert | String | Device certificate, used to authenticate the client when establishing a TLS connection. This parameter will be returned if asymmetric encryption is used |
| DevicePrivateKey | String | Private key of the device, used to authenticate the client when establishing a TLS connection. It is not saved in Tencent Cloud's backend. Please keep it safe. This parameter will be returned if asymmetric encryption is used |
| LoraDevEui | String | DevEui of a LoRa device. This field will be returned if the device is a LoRa device |
| LoraMoteType | Integer | MoteType of a LoRa device. This field will be returned if the device is a LoRa device |
| LoraAppKey | String | AppKey of a LoRa device. This field will be returned if the device is a LoRa device |
| LoraNwkKey | String | NwkKey of a LoRa device. This field will be returned if the device is a LoRa device |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Creating a Device (Using Asymmetric Encryption)

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=CreateDevice
&ProductId=ABCDE12345
&DeviceName=test_device
&Attribute.Tags.0.Tag=note
&Attribute.Tags.0.Type=2
&Attribute.Tags.0.Value=test_note
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "DevicePrivateKey": "xxxxxxxxxxxxxxxxxxxxxxx",
    "DeviceName": "test_device",
    "DevicePsk": "",
    "LoraDevEui": "",
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "DeviceCert": "xxxxxxxxxxxxxxxxxxxx",
    "LoraMoteType": ""
  }
}
```

### Example 2. Creating a Device (Using Symmetric Encryption)

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=CreateDevice
&ProductId=ABCDE12345
&DeviceName=test_device
&Attribute.Tags.0.Tag=note
&Attribute.Tags.0.Type=2
&Attribute.Tags.0.Value=test_note
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "DevicePrivateKey": "",
    "DeviceName": "test_device",
    "DevicePsk": "xxxxxxxxxxxxx",
    "LoraDevEui": "",
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "DeviceCert": "",
    "LoraMoteType": ""
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=CreateDevice)

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
| InvalidParameterValue.DeviceAlreadyExist | Name of the created device already exists. |
| LimitExceeded.DeviceExceedLimit | Number of devices exceeds the limit. |
| ResourceNotFound.ProductNotExist | Product does not exist. |
| UnauthorizedOperation.ProductCantHaveLoRaDevice | This product type cannot create LoRa devices. |
| UnauthorizedOperation.ProductCantHaveNotLoRaDevice | This product type can only create LoRa devices. |
| UnauthorizedOperation.ProductNotSupportPSK | The product does not support key-based authentication. |
