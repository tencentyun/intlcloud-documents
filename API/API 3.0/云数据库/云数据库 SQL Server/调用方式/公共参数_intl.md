Common parameters are used for user identification and API authentication. Unless necessary, these parameters will not be discussed in each API document. A request must contain these parameters to be initiated successfully.

| Parameter Name | Type | Required | Description |
|:---------|:---------|:-----|:---- |
| Action | String | Yes | The name of the API for the operation to be performed. For example, if you want to call the CVM API "Query Instance List", the Action parameter is DescribeInstances. |
| Region | String | Yes | Identifies the region to which the data you want to work with belongs. |
| Timestamp | Integer | Yes | Indicates the time when the API request was initiated. It is expressed in a UNIX timestamp, for example, 1529223702. If the difference between the value and the current system time is too large, a signature expiration error may occur. |
| Nonce | Integer | Yes | A random positive integer used in conjunction with Timestamp to prevent replay attacks. |
| SecretId | String | Yes | An ID that the user applies for on the <a href="https://console.cloud.tencent.com/capi">Cloud API Key</a> console for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request Signature. |
| Signature | String | Yes | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information on how to compute the signature, see the documentation about API authentication. |
| Version | String | Yes | API version, such as 2017-03-12 |
| SignatureMethod | String | No | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. |
| Token | String | No | The token used for a temporary certificate. It must be used with a temporary key. You can obtain the temporary key and token by calling a CAM API. No token is required for a long-term key. |


If, for example, you want to query the list of CVM instances in the Guangzhou region, the request URL is as follows:

<pre>
https://cvm.tencentcloudapi.com/?Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1402992826
&Nonce=345122
&Signature=xxxxxxxx
&Version=2017-03-12
</pre>


## Region List

The supported Region field values for all APIs in this product are listed as below. For any API that does not support any of the following regions, this field will be described additionally in the relevant API document.


| Region | Value |
|------|------|
| North China (Beijing) | ap-beijing |
| South China (Guangzhou) | ap-guangzhou |
| Southeast Asia (Hong Kong) | ap-hongkong |
| East China (Shanghai) | ap-shanghai |
| East China (Shanghai Finance) | ap-shanghai-fsi |
| South China (Shenzhen Finance) | ap-shenzhen-fsi |

