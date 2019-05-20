The common parameters are used to authenticate the user and API. If not necessary, these parameters are not described in individual API documents. However, they have to be carried by each request to initiate properly.
## Signature Method v3
When the TC3-HMAC-SHA256 signature method is used, the common parameters should be uniformly placed in the HTTP request header as shown below:
| Parameter name | Type | Required | Description |
|--------|----|----|----|
| X-TC-Action | String | Yes | The name of the command API for the specific operation. For example, if you want to call the instance list query API of Cloud Virtual Machine, then the Action parameter is DescribeInstances. |
| X-TC-Region | String | Yes | The Region parameter used to identify the region whose data you want to operate on. |
| X-TC-Timestamp | Integer | Yes | The current UNIX timestamp which records when an API request is initiated. For example, 1529223702. If it is more than 5 minutes different from the current time on the API server, it will cause a signature expiry error. |
| X-TC-Version | String | Yes | The version of the API. For example, 2017-03-12. |
| Authorization | String | Yes | Header field of the standard authentication of the HTTP request, for example: <br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 <br/>Here, <br/>- TC3-HMAC-SHA256: Signature method, currently fixed as this value; <br/>- Credential: Signature credential; AKIDEXAMPLE is the SecretId; Date is a date in UTC time, whose value should match the UTC date converted by the common parameter X-TC-Timestamp; service is the product name, which should match the domain name of the product called, such as cvm; <br/>- SignedHeaders: Information of the headers involving in the signature; content-type and host are required headers; <br/>- Signature: Signature summary. |
| X-TC-Token | String | No | The token used by the temporary certificate, which needs to be used in conjunction with the temporary key. The temporary key and token need to be obtained through the access management service call API. Long-term keys do not require a token. |
Assuming you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, the request structure in the form of request URL, request header and request body may be as follows:
Example of an HTTP GET request structure:
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
Example of an HTTP POST (application/json) request structure:
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
Example of an HTTP POST (multipart/form-data) request structure (only supported by specific APIs):
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
When the HmacSHA1 or HmacSHA256 signature method is used, the common parameters should be uniformly placed in request string as shown below:
| Parameter name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| Action | String | Yes | The name of the command API for the specific operation. For example, if you want to call the instance list query API of Cloud Virtual Machine, then the Action parameter is DescribeInstances. |
| Region | String | Yes | The Region parameter used to identify the region whose data you want to operate on. |
| Timestamp | Integer | Yes | The current UNIX timestamp which records when an API request is initiated. For example, 1529223702. If it is too different from the current time, it will cause a signature expiry error. |
| Nonce | Integer | Yes | A random positive integer used to prevent replay attacks along with Timestamp. |
| SecretId | String | Yes | The identifying SecretId obtained on the [Cloud API Key](https://console.cloud.tencent.com/capi) page. A SecretId corresponds to a unique SecretKey which is used to generate the request signature (Signature). |
| Signature | String | Yes | Request signature used to verify the validity of this request. This is calculated based on the actual input parameters. For details on how to calculate, see the API authentication document. |
| Version | String | Yes | The version of the API. For example, 2017-03-12. |
| SignatureMethod | String | No | Signature method. Currently, only HmacSHA256 and HmacSHA1 are supported. The HmacSHA256 algorithm is used to verify the signature only when this parameter is specified as HmacSHA256. In other cases, the signature is verified with HmacSHA1. |
| Token | String | No | The token used by the temporary certificate, which needs to be used in conjunction with the temporary key. The temporary key and token need to be obtained through the access management service call API. Long-term keys do not require a token. |
Assuming you want to query the list of Cloud Virtual Machine instances in the Guangzhou region, the request structure in the form of request URL, request header and request body may be as follows:
Example of an HTTP GET request structure:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```
Example of an HTTP POST request structure:
```
https://cvm.tencentcloudapi.com/
Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```
## Region List
The possible values for the Region field in all APIs of this product are as shown below. If an API does not support any of the listed regions, the detail will be described separately in the API documentation.
| Region | Value |
|------|------|
|North China (Beijing)|ap-beijing|
|Southwest China (Chengdu)|ap-chengdu|
|South China (Guangzhou)|ap-guangzhou|
|South China (Guangzhou Open)|ap-guangzhou-open|
|Asia Pacific (Mumbai)|ap-mumbai|
|East China (Shanghai)|ap-shanghai|

