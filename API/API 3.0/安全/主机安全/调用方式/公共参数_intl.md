Common parameters are used for user identification and API authentication. Unless necessary, these parameters will not be discussed in each API document. A request must contain these parameters to be initiated successfully.

## Signature Method v3

To adopt the TC3-HMAC-SHA256 signature method, common parameters must be put into the HTTP Header request header, as shown below:

| Parameter Name | Type | Required | Description |
|--------|----|----|----|
| X-TC-Action | String | Yes | The name of the API for the operation to be performed. For example, if you want to call the CVM API "Query Instance List", the Action parameter is DescribeInstances. |
| X-TC-Region | String | Yes | Identifies the region to which the data you want to work with belongs |
| X-TC-Timestamp | Integer | Yes | Indicates the time when the API request was initiated. It is expressed in a UNIX timestamp, for example, 1529223702. If the time difference between the unix timestamp and the API server is greater than 5 minutes, a signature expiration error may occur. |
| X-TC-Version | String | Yes | API version, such as 2017-03-12 |
| Authorization | String | Yes | Header field of HTTP standard identity verification, such as<br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024. <br/><br/>- TC3-HMAC-SHA256: signature method. This value is used.<br/>- Credential: signature credentials. AKIDEXAMPLE is SecretId; Date is UTC date, which must be consistent with the UTC date converted by the X-TC-Timestamp common parameter; service is the product name, which must be consistent with the called product domain name, such as CVM;<br/>- SignedHeaders: Header information for signature computing. The content-type and host are required;<br/>- Signature: signature digest. |
| X-TC-Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |

If, for example, you want to query the list of CVM instances in the Guangzhou region, the request URL is as follows:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5
da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

## Signature Method v1

To adopt the HmacSHA1 and HmacSHA256 signature methods, common parameters must be put into the request string, as shown below:

| Parameter Name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| Action | String | Yes | The name of the API for the operation to be performed. For example, if you want to call the CVM API "Query Instance List", the Action parameter is DescribeInstances. |
| Region | String | Yes | Identifies the region to which the data you want to work with belongs |
| Timestamp | Integer | Yes | Indicates the time when the API request was initiated. It is expressed in a UNIX timestamp, for example, 1529223702. If the difference between the value and the current system time is too large, a signature expiration error may occur. |
| Nonce | Integer | Yes | A random positive integer used in conjunction with Timestamp to prevent replay attacks |
| SecretId | String | Yes | An ID that the user applies for on the <a href="https://console.cloud.tencent.com/capi">Cloud API Key</a> console for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request Signature. |
| Signature | String | Yes | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information on how to compute the signature, see the documentation about API authentication. |
| Version | String | Yes | API version, such as 2017-03-12. |
| SignatureMethod | String | No | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. |
| Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |


If, for example, you want to query the list of CVM instances in the Guangzhou region, the request URL is as follows:

```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1402992826
&Nonce=345122
&Signature=xxxxxxxx
&Version=2017-03-12
```

