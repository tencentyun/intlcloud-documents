## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（CreateCertificate）用于创建Gaap相关证书和配置文件，包括基础认证配置文件，客户端CA证书，服务器SSL证书，Gaap SSL证书以及源站CA证书。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateCertificate |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| CertificateType | 是 | Integer | 证书类型。其中：<br/>0，表示基础认证配置；<br/>1，表示客户端CA证书；<br/>2，服务器SSL证书；<br/>3，表示源站CA证书；<br/>4，表示通道SSL证书。 |
| CertificateContent | 是 | String | 证书内容。采用url编码。其中：<br/>当证书类型为基础认证配置时，该参数填写用户名/密码对。格式：“用户名：密码”，例如：root:FSGdT。其中密码使用htpasswd或者openssl，例如：openssl passwd -crypt 123456。<br/>当证书类型为CA/SSL证书时，该参数填写证书内容，格式为pem。 |
| CertificateAlias | 否 | String | 证书名称 |
| CertificateKey | 否 | String | 秘钥内容。采用url编码。仅当证书类型为SSL证书时，需要填写该参数。格式为pem。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| CertificateId | String | 证书ID|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建证书

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=CreateCertificate
&CertificateAlias=xxx
&CertificateType=2
&CertificateContent=%0A-----BEGIN%20CERTIFICATE-----%0AMIIFmDCCBICgAwIBAgIQC6TGAPV%2B4MO7NIhlkkKFljANBgkqhkiG9w0BAQsFADBy%0AMQswCQYDVQQGEwJDTjElMCMGA1UEChMcVHJ1c3RBc2lhIFRlY2hub2xvZ2llcywg%0ASW5jLjEdMBsGA1UECxMURG9tYWluIFZhbGlkYXRlZCBTU0wxHTAbBgNVBAMTFFRy%0AdXN0QXNpYSBUTFMgUlNBIENBMB4XDTE5MDQwMjAwMDAwMFoXDTIwMDQwMTEyMDAw%0AMFowGTEXMBUGA1UEAxMObGFnYW1lZnQwMS54eXowggEiMA0GCSqGSIb3DQEBAQUA%0AA4IBDwAwggEKAoIBAQCuSgglfAksbFSrvWp6cEFr8ulTWEND2KvXf6cCs3kBBCzE%0AMLhCw4792LMFY0%2BFE7a0j7i5nJ9%2BQvhX7GRiu1P9flyge0eUCOBOAtVCn0dvhbLy%0A7efWsmH3kp/owWXnZXeb/k5R1FvojCiV968MxMC%2B2Y7ejz5qMm5XlQPn3xQOEj2h%0AQmHwQ9XwO8qRsIuCD1oNrsXsyXuEhA2zkEvcgtYP35zPsXfjbBaBg7Iw3o0j3jXj%0AgdhD2Q2OzH05jDn3hDhSnej1jbWuGmDEOO%2Bu6W/xqnCOhBMjWLnuW2aUddiBiqsH%0A8BQK/Ge6HUp%2BmMdkdNAw5FN6ztIPzP6GFb0OOLitAgMBAAGjggKBMIICfTAfBgNV%0AHSMEGDAWgBR/05nzoEcOMQBWViKOt8ye3coBijAdBgNVHQ4EFgQUqYL1l3uFqYHC%0A2mJcZC26nLHtkjYwLQYDVR0RBCYwJIIObGFnYW1lZnQwMS54eXqCEnd3dy5sYWdh%0AbWVmdDAxLnh5ejAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEG%0ACCsGAQUFBwMCMEwGA1UdIARFMEMwNwYJYIZIAYb9bAECMCowKAYIKwYBBQUHAgEW%0AHGh0dHBzOi8vd3d3LmRpZ2ljZXJ0LmNvbS9DUFMwCAYGZ4EMAQIBMH0GCCsGAQUF%0ABwEBBHEwbzAhBggrBgEFBQcwAYYVaHR0cDovL29jc3AuZGNvY3NwLmNuMEoGCCsG%0AAQUFBzAChj5odHRwOi8vY2FjZXJ0cy5kaWdpdGFsY2VydHZhbGlkYXRpb24uY29t%0AL1RydXN0QXNpYVRMU1JTQUNBLmNydDAJBgNVHRMEAjAAMIIBAwYKKwYBBAHWeQIE%0AAgSB9ASB8QDvAHUAu9nfvB%2BKcbWTlCOXqpJ7RzhXlQqrUugakJZkNo4e0YUAAAFp%0A3cON9gAABAMARjBEAiABFpvdLsJKm6zxh5wLS6uN5%2BTnX8bXD5bj7CPVC4Kg/wIg%0AB%2BBzdsZL0UmuvbNAYkr8W53bJKhEgoHJ0RdSyoF5yZAAdgCHdb/nWXz4jEOZX73z%0Abv9WjUdWNv9KtWDBtOr/XqCDDwAAAWndw47mAAAEAwBHMEUCIQC%2BDdvaJ2kKvsVv%0AiivLe4W/YFa/K64HdnyOdHksEl9pSAIgTqLXfw6Tc7d%2BgiKMtt%2B6P/xdrvjGt5Du%0Aokvgu70INuQwDQYJKoZIhvcNAQELBQADggEBAHxewHgySBS5UoO6l/IcU95baR/O%0AYGLcCpgEbWj4MigIZcrkHsD7RddRDoyM/3hxKyzs3Dkes4wHTQDWnyrNuXdn8aNV%0AJAhrh/0yzAe3/UTJ/%2BSRoMg1K6rHWORmLa52d9u3Ei%2B1BF2qLi5L2tTmLrSQJXzB%0ANSIFd40x1mZLp9uqhcB9kcwwkHSFUtLjFwUSN6Zjn9FStlq06ezjgnVv2tP9/HoP%0AKWiRgRFDgqj8%2BROJPQvfuO2xdWoxYUmuMcx1o6IiSVn2F48ood029cyT%2Bt3TaYpb%0AhVI9JuYnHW9kN69xPNzamJVCdu4i/1ELvcr0p/wQf9ax63XsgX4YYhdYgMQ%3D%0A-----END%20CERTIFICATE-----%0A-----BEGIN%20CERTIFICATE-----%0AMIIErjCCA5agAwIBAgIQBYAmfwbylVM0jhwYWl7uLjANBgkqhkiG9w0BAQsFADBh%0AMQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3%0Ad3cuZGlnaWNlcnQuY29tMSAwHgYDVQQDExdEaWdpQ2VydCBHbG9iYWwgUm9vdCBD%0AQTAeFw0xNzEyMDgxMjI4MjZaFw0yNzEyMDgxMjI4MjZaMHIxCzAJBgNVBAYTAkNO%0AMSUwIwYDVQQKExxUcnVzdEFzaWEgVGVjaG5vbG9naWVzLCBJbmMuMR0wGwYDVQQL%0AExREb21haW4gVmFsaWRhdGVkIFNTTDEdMBsGA1UEAxMUVHJ1c3RBc2lhIFRMUyBS%0AU0EgQ0EwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCgWa9X%2Bph%2BwAm8%0AYh1Fk1MjKbQ5QwBOOKVaZR/OfCh%2BF6f93u7vZHGcUU/lvVGgUQnbzJhR1UV2epJa%0Ae%2Bm7cxnXIKdD0/VS9btAgwJszGFvwoqXeaCqFoP71wPmXjjUwLT70%2BqvX4hdyYfO%0AJcjeTz5QKtg8zQwxaK9x4JT9CoOmoVdVhEBAiD3DwR5fFgOHDwwGxdJWVBvktnoA%0AzjdTLXDdbSVC5jZ0u8oq9BiTDv7jAlsB5F8aZgvSZDOQeFrwaOTbKWSEInEhnchK%0AZTD1dz6aBlk1xGEI5PZWAnVAba/ofH33ktymaTDsE6xRDnW97pDkimCRak6CEbfe%0A3dXw6OV5AgMBAAGjggFPMIIBSzAdBgNVHQ4EFgQUf9OZ86BHDjEAVlYijrfMnt3K%0AAYowHwYDVR0jBBgwFoAUA95QNVbRTLtm8KPiGxvDl7I90VUwDgYDVR0PAQH/BAQD%0AAgGGMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjASBgNVHRMBAf8ECDAG%0AAQH/AgEAMDQGCCsGAQUFBwEBBCgwJjAkBggrBgEFBQcwAYYYaHR0cDovL29jc3Au%0AZGlnaWNlcnQuY29tMEIGA1UdHwQ7MDkwN6A1oDOGMWh0dHA6Ly9jcmwzLmRpZ2lj%0AZXJ0LmNvbS9EaWdpQ2VydEdsb2JhbFJvb3RDQS5jcmwwTAYDVR0gBEUwQzA3Bglg%0AhkgBhv1sAQIwKjAoBggrBgEFBQcCARYcaHR0cHM6Ly93d3cuZGlnaWNlcnQuY29t%0AL0NQUzAIBgZngQwBAgEwDQYJKoZIhvcNAQELBQADggEBAK3dVOj5dlv4MzK2i233%0AlDYvyJ3slFY2X2HKTYGte8nbK6i5/fsDImMYihAkp6VaNY/en8WZ5qcrQPVLuJrJ%0ADSXT04NnMeZOQDUoj/NHAmdfCBB/h1bZ5OGK6Sf1h5Yx/5wR4f3TUoPgGlnU7EuP%0AISLNdMRiDrXntcImDAiRvkh5GJuH4YCVE6XEntqaNIgGkRwxKSgnU3Id3iuFbW9F%0AUQ9Qqtb1GX91AJ7i4153TikGgYCdwYkBURD8gSVe8OAco6IfZOYt/TEwii1Ivi1C%0AqnuUlWpsF1LdQNIdfbW3TSe0BhQa7ifbVIfvPWHYOu3rkg1ZeMo6XRU9B4n5VyJY%0ARmE%3D%0A-----END%20CERTIFICATE-----%0A
&CertificateKey=%0A-----BEGIN%20RSA%20PRIVATE%20KEY-----%0Axxxxxxxxxxx%0A-----END%20RSA%20PRIVATE%20KEY-----%0A
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "c7bfcad5-3f20-472f-9afc-13a66faebad8",
    "CertificateId": "cert-xxx"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=CreateCertificate)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/608/36938#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.InvalidCertificateContent | 解析失败，请检查证书内容格式。 |
| InvalidParameterValue.InvalidCertificateKey | 解析失败，请检查证书密钥格式。 |
| MissingParameter | 缺少参数错误 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
| UnsupportedOperation | 不支持该操作。 |
