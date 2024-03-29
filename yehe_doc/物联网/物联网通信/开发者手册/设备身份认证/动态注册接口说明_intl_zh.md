## 参数说明

设备动态注册时需携带 ProductId 和 DeviceName 向平台发起`http/https`请求，请求接口及参数如下：

- 请求的 URL 为：
  ``
  https://ap-guangzhou.gateway.tencentdevices.com/device/register
  ``
  ``
  http://ap-guangzhou.gateway.tencentdevices.com/device/register
  ``

- 请求方式：Post

### 请求参数

| 参数名称   | 必选 | 类型   | 描述     |
| ---------- | ---- | ------ | -------- |
| ProductId  | 是   | string | 产品 Id  |
| DeviceName | 是   | string | 设备名称 |

>? 接口只支持 application/json 格式。

### 签名生成

使用 HMAC-sha256 算法对请求报文进行签名，详情请参见 [签名方法](https://intl.cloud.tencent.com/document/product/1105/41501)。

### 平台返回参数

| 参数名称  | 类型   | 描述                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| RequestId | String | 请求 Id                                                      |
| Len       | Int64  | 返回的 Payload 长度                                            |
| Payload   | String | 返回的设备注册信息。该数据通过加密后返回，需要设备端自行解密处理 |

>? 加密过程是将原始 json 格式的 Payload 转为字符串后进行 AES 加密，再进行 base64 加密。AES 加密算法为 CBC 模式，密钥长度128，取 productSecret 前16位，偏移量为长度16的字符“0”。
>

原始 Payload 内容说明：

| key            | value      | 描述                                                       |
| -------------- | ---------- | ---------------------------------------------------------- |
| encryptionType | 1          | 加密类型。<li>1表示证书认证<li>2表示密钥认证                     |
| psk            | 1239466501 | 设备密钥，当产品认证类型为密钥认证时有此参数               |
| clientCert     | -          | 设备证书文件字符串格式，当产品认证类型为证书认证时有此参数 |
| clientKey      | -          | 设备私钥文件字符串格式，当产品认证类型为证书认证时有此参数 |

## 示例代码

#### 请求包

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

#### 返回包

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


#### Payload 数据解析示例

>?以下数据仅提供您进行测试使用，在您正式使用时，请务必保证您的信息不被泄露。

1. Payload 原始内容为
```
s6FB3a1BA/YYbcmSE12XpeDVmQNDcf1QgVD141RRbmmAnFwQfp1ECAu5O016mCOvYlJJ6V59yM4OqQSiWphfTg==
```
2. Base64 解码后
```
b3a141ddad4103f6186dc992135d97a5e0d599034371fd508150f5e354516e69809c5c107e9d44080bb93b4d7a9823af625249e95e7dc8ce0ea904a25a985f4e
```
3. AES 解密
 - 产品密钥：`hzvf5LF9S0isvBhDSauWMaIk`
 - 解密后数据：`{"encryptionType":2,"psk":"lDZ6Uqt+I9E0wW7rvDUs7Q=="}`







