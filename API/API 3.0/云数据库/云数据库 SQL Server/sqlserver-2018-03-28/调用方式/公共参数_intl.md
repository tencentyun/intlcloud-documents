The common parameters are used to authenticate the user and API. If not necessary, these parameters are not described in individual API documents. However, they have to be carried by each request to initiate properly.

## Signature Method v3

When using TC3-HMAC-SHA256 to sign your requests, you should include all common parameters in the HTTP header as shown below:

| Parameter name | Type | Required | Description |
|--------|----|----|----|
| X-TC-Action | String | Yes | API name of the action. For the valid values, see the description of the common input parameter "Action" in the API documentation. For example, the value of the CVM instance list querying API is DescribeInstances. |
| X-TC-Region | String | Yes | A parameter for specifying the region of the operated data. For the valid regions, see the description of the common input parameter "Region" in the API documentation. Note: This parameter is not required by some APIs and will not be in effect when using these APIs. You can find the detailed information about optional parameters in the API documentation. |
| X-TC-Timestamp | Integer | Yes | The current UNIX timestamp. It records the time when an API request is initiated. For example, 1529223702. Note: A greater-than-5-minute difference between your local current time and the API server time can cause your signature to expire. |
| X-TC-Version | String | Yes | API version of the action. For the valid values, see the description of the common input parameter "Version" in the API documentation. For example, the version of CVM is 2017-03-12. |
| Authorization | String | Yes | The HTTP authentication request header, for example: <br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 <br/>Here, <br/>- TC3-HMAC-SHA256: Signature method, currently fixed as this value; <br/>- Credential: Signature credential; EXAMPLE is the SecretId; Date is a date in UTC time, and this value must be matched the value of X-TC-Timestamp (a common parameter) in UTC time format; service is the name of the product/service (e.g., cvm) you called; <br/>- SignedHeaders: The headers that contains the authentication information; content-type and host are the required headers; <br/>- Signature: Signature digest. |
| X-TC-Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |

Assume that you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, structure a request that consists of the request URL, the request header and request body as follows:

Sample of an HTTP GET request structure:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKID**********************0123456789EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

Sample of an HTTP POST (application/json) request structure:

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

Sample of an HTTP POST (multipart/form-data) request structure (only supported by specific APIs):

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

When using HmacSHA1 or HmacSHA256 to sign your requests, you should include all common parameters in the HTTP header as shown below:

| Parameter name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| X-TC-Action | String | Yes | API name of the action. For the valid values, see the description of the common input parameter "Action" in the API documentation. For example, the value of the CVM instance list querying API is DescribeInstances. |
| Region | String | Yes | A parameter for specifying the region of the operated data. For the valid regions, see the description of the common input parameter "Region" in the API documentation. Note: This parameter is not required by some APIs and will not be in effect when using these APIs. You can find the detailed information about optional parameters in the API documentation. |
| Timestamp | Integer | Yes | The current UNIX timestamp. It records the time when an API request is initiated. For example, 1529223702. Note: If the difference between this value and the current time is too large, your signature will be expired. |
| Nonce | Integer | Yes | A random positive integer used along with Timestamp to prevent replay attacks. |
| SecretId | String | Yes | You can obtain your SecretId here [TencentCloud API Key](https://console.cloud.tencent.com/capi). A SecretId is a unique identifier of a SecretKey which is used to generate a signature for your request. |
| Signature | String | Yes | The signature added in the HTTP request for verifying the identity of the requester. The signature is calculated based on the actual input parameters. |
| Version | String | Yes | API version of the action. For the valid values, see the description of the common input parameter "Version" in the API documentation. For example, the version of CVM is 2017-03-12. |
| SignatureMethod | String | No | Keyed hash algorithm that is used to create a signature. You may use either HmacSHA256 or HmacSHA1. However, you only use HmacSHA256 when specified. |
| Token | String | No | The token that is used along with the temporary key to generate the temporary certificate. You need to obtain the temporary key and token by calling the CAM API. A token is not required when a long-term key is being used. |


Assume that you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, structure a request that consists of the request URL, the request header and request body as follows:

Sample of an HTTP GET request structure:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

Sample of an HTTP POST request structure:

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
|North China (Beijing)|ap-beijing|
|South China (Guangzhou)|ap-guangzhou|
|Southeast Asia (Hong Kong, China)|ap-hongkong|
|East China (Shanghai)|ap-shanghai|

