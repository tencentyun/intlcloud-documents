In order to complete a Tencent Cloud API request, you need to set up two types of request parameters: common request parameter and API request parameter. This document describes 6 common request parameters that are used in Tencent Cloud API requests. For more information on API request parameters, see API Request Parameters.
Common request parameters are required in every API. When you use Tencent Cloud APIs to send requests, you have to make sure that you are passing along the common request parameters. Otherwise, the requests will fail. You also have to make sure to capitalize the first letters of common request parameters so that they can be differentiated from API request parameters.

Common request parameters are as follows:

| Parameter Name | Required | Type | Description |
| ------------ | ------------ | ------------ | ------------ |
| Action | Yes | String | The name of the API for the desired operation. For example, if you want to call the API to get temporary access credentials for federated identities, choose GetFederationToken. |
| Region | No | String | Region parameter, which is used to identify the region where you want to get STS service . Notes: 1. Only ap-guangzhou and ap-shanghai are available to all users, and STS services in other regions are still in beta. 2. If the region is missing, then use "ap-guangzhou" as default|
| Timestamp | Yes | UInt | The current UNIX timestamp that records the time at which the API request was initiated. |
| Nonce | Yes | UInt | A random positive integer that is used in conjunction with Timestamp to prevent replay attacks. |
| SecretId | Yes | String | An ID that the user applies for on the [Cloud API Key](https://intl.cloud.tencent.com/login) for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request signature. For more information, see [Signature Method](https://intl.cloud.tencent.com/document/api/377/4214). |
| Signature | Yes | String | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information, see [Signature Method](https://intl.cloud.tencent.com/document/api/377/4214). |
| SignatureMethod | Yes | String | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. For more information, see [Signature Method](https://intl.cloud.tencent.com/document/api/377/4214). |


**Example**

The following example shows how a common request parameter looks like in an Tencent Cloud API request. For example, if you want to query the list of Tencent Cloud CVM instances in Guangzhou regions, the desired request format is:
```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<API request parameters>
```

