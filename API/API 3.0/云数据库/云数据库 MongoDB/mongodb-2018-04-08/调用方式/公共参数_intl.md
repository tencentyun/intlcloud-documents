Common parameters are used for user identification and API authentication. Unless necessary, these parameters will not be discussed in each API document. A request must contain these parameters to be initiated successfully.

## Signature Method v3

To adopt the TC3-HMAC-SHA256 signature method, common parameters must be put into the HTTP Header request header, as shown below:

| Parameter Name | Type | Required | Description |
|--------|----|----|----|
| X-TC-Action | String | Yes | The name of the API for the operation to be performed. For example, if you want to call the CVM API "Query Instance List", the Action parameter is DescribeInstances. |
| X-TC-Region | String | Yes | Identifies the region to which the data you want to work with belongs |
| X-TC-Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, for example, 1529223702. If the difference between the UNIX timestamp and the API server time is greater than 5 minutes, a signature expiration error may occur. |
| X-TC-Version | String | Yes | API version, such as 2017-03-12 |
| Authorization | String | Yes | Header field of HTTP standard identity authentication, such as:<br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024.<br/><br/>- TC3-HMAC-SHA256: signature method. This value is always used.<br/>- Credential: signature credentials. AKIDEXAMPLE is SecretId; Date is UTC date, which must be consistent with the UTC date converted by the X-TC-Timestamp common parameter; service is the product name, which must be consistent with the called product domain name, such as CVM;<br/>- SignedHeaders: Header information for signature computing. The content-type and host are required;<br/>- Signature: signature digest. |
| X-TC-Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |

If, for example, you want to query the list of CVM instances in the Guangzhou region, the request contains the request URL, request header and request body, as shown below:

Example of an HTTP GET request:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

Example of an HTTP POST (application/json) request:

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: application/json
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

{"Offset":0,"Limit":10}
```

Example of an HTTP POST (multipart/form-data) request (only supported by specific APIs):

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: multipart/form-data; boundary=58731222010402
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

--58731222010402
Content-Disposition: form-data; name="Offset"

0
--58731222010402
Content-Disposition: form-data; name="Limit"

10
--58731222010402--
```

## Signature Method v1

To adopt the HmacSHA1 and HmacSHA256 signature methods, common parameters must be put into the request string, as shown below:

| Parameter Name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| Action | String | Yes | The name of the API for the operation to be performed. For example, if you want to call the CVM API "Query Instance List", the Action parameter is DescribeInstances. |
| Region | String | Yes | Identifies the region to which the data you want to work with belongs |
| Timestamp | Integer | Yes | The current UNIX timestamp that records the time when the API request was initiated, for example, 1529223702. If the difference between the value and the current system time is too large, a signature expiration error may occur. |
| Nonce | Integer | Yes | A random positive integer used in conjunction with Timestamp to prevent replay attacks |
| SecretId | String | Yes | An ID that the user applies for on the <a href="https://console.cloud.tencent.com/capi">Cloud API Key</a> Console for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request Signature. |
| Signature | String | Yes | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information on how to compute the signature, see the documentation about API authentication. |
| Version | String | Yes | API version, such as 2017-03-12. |
| SignatureMethod | String | No | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. |
| Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |


If, for example, you want to query the list of CVM instances in the Guangzhou region, the request contains the request URL, request header and request body, as shown below:

Sample of an HTTP GET request:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

Sample of an HTTP POST request:

```
https://cvm.tencentcloudapi.com/

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded

Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```


## Region List

The supported Region field values for all APIs in this product are listed as below. For any API that does not support any of the following regions, this field will be described additionally in the relevant API document.


| Region | Value |
|------|------|
| Asia Pacific (Bangkok) | ap-bangkok|
| North China (Beijing) | ap-beijing |
| Southwest China (Chengdu) | ap-chengdu |
| Southwest China (Chongqing) | ap-chongqing|
| South China (Guangzhou) | ap-guangzhou |
| Southeast Asia (Hong Kong) | ap-hongkong |
| Asia Pacific (Mumbai) | ap-mumbai |
| Asia Pacific (Seoul) | ap-seoul |
| East China (Shanghai) | ap-shanghai |
| East China (Shanghai Finance) | ap-shanghai-fsi |
| South China (Shenzhen Finance) | ap-shenzhen-fsi |
| Southeast Asia (Singapore) | ap-singapore |
| Asia Pacific (Tokyo) | ap-tokyo |
| Europe (Frankfurt) | eu-frankfurt |
| Europe (Moscow) | eu-moscow |
| Eastern U.S. (Virginia) | na-ashburn |
| Western U.S. (Silicon Valley) | na-siliconvalley |
| North America (Toronto) | na-toronto |

