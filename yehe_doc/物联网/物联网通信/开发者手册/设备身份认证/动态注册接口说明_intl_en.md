## Parameter Description

When a device is dynamically registered, it needs to carry `ProductId` and `DeviceName` to initiate an `http/https` request to the platform. The request API and parameters are as detailed below:

- Requested URL:
  ``
  https://ap-guangzhou.gateway.tencentdevices.com/device/register
  ``
  ``
  http://ap-guangzhou.gateway.tencentdevices.com/device/register
  ``

- Request method: POST

### Request parameters

| Parameter | Required | Type | Description |
| ---------- | ---- | ------ | -------- |
| ProductId | Yes | string | Product ID |
| DeviceName | Yes | string | Device name |

>? The API only supports the `application/json` format.

### Signature generation

Use the HMACSHA256 algorithm to sign the request message. For more information, please see [Signature Algorithm](https://intl.cloud.tencent.com/document/product/1105/41501).

### Platform response parameters

| Parameter | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| RequestId | String | Request ID |
| Len | Int64 | Length of the returned payload |
| Payload | String | Returned device registration information, which is encrypted and needs to be decrypted and processed by the device itself |

>? The encryption process is to convert the raw payload in JSON format into a string, perform AES encryption on it, and then perform Base64 encryption on it. The AES encryption algorithm is CBC mode, where the key length is 128 bits, the first 16 bits of `productSecret` are taken, and the offset is the character "0" with a length of 16 bits.
>

Raw payload content description:

| Key | Value | Description |
| -------------- | ---------- | ---------------------------------------------------------- |
| encryptionType | 1 | Encryption type. <li>1: certificate authentication<li>2: key authentication |
| psk | 1239466501 | Device key. This parameter is available when the product authentication type is key authentication. |
| clientCert | - | String format of device certificate file. This parameter is available when the product authentication type is certificate authentication. |
| clientKey | - | String format of device private key file. This parameter is available when the product authentication type is certificate authentication. |

## Sample Code

#### Request packet

```
POST https://ap-guangzhou.gateway.tencentdevices.com/device/register
Content-Type: application/json
Host: ap-guangzhou.gateway.tencentdevices.com
X-TC-Algorithm: HmacSha256
X-TC-Timestamp: 1551****65
X-TC-Nonce: 5456
X-TC-Signature: 2230eefd229f582d8b1b891af7107b91597****07d778ab3738f756258d7652c
{"ProductId":"ASJ****GX","DeviceName":"xyz"}
```

#### Response packet

<dx-codeblock>
:::  json
{
  "Response": {
    "Len": 53,
    "Payload": "031T01DWAoqFePDt71VuZXuLzkUzbIhGOnvMzpAFtNgOjagyFNHVSostNl9ztvhOuRx0dMM/DMoWAXQCfL7jyA==",
    "RequestId": "f4da4f1f-d72e-40f1-****-349fc0072ba0"
  }
}
:::
</dx-codeblock>


#### Payload data parsing sample

>?The following data is for test only. When you use it formally, please ensure that your information is not leaked.

1. The raw payload content is:
```
s6FB3a1BA/YYbcmSE12XpeDVmQNDcf1QgVD141RRbmmAnFwQfp1ECAu5O016mCOvYlJJ6V59yM4OqQSiWphfTg==
```
2. After Base64-decoding:
```
b3a141ddad4103f6186dc992135d97a5e0d599034371fd508150f5e354516e69809c5c107e9d44080bb93b4d7a9823af625249e95e7dc8ce0ea904a25a985f4e
```
3. AES decryption:
 - Product key: `hzvf5LF9S0isvBhDSauWMaIk`
 - Data after decryption: `{"encryptionType":2,"psk":"lDZ6Uqt+I9E0wW7rvDUs7Q=="}`







