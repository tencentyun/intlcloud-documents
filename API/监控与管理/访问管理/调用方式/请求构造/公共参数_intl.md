A complete Tencent Cloud API request requires two types of request parameters: common request parameter and API request parameter. This document describes 6 common request parameters used in Tencent Cloud API requests. For more information on API request parameters, see API Request Parameters.
Common request parameters are required in every API. When developers use Tencent Cloud APIs to send requests, they should make sure that the requests carry these common request parameters. Otherwise, the requests will fail. The first letter of each common request parameter is in uppercase so that the parameter can be differentiated from API request parameters.

Common request parameters are as follows:

| Parameter Name | Required | Type | Description |
| ------------ | ------------ | ------------ | ------------ |
| Action | Yes | String | The name of the API for the desired operation. For example, if you want to call the API for getting temporary access credentials for user with federated identity, the Action parameter is GetFederationToken. |
| Region | No | String | Region parameter, which is used to identify the region to which the STS service you want to use belongs. Notes: 1. Only ap-guangzhou and ap-shanghai are available to all users, and STS services in other regions are still in trial. 2. It defaults to ap-guangzhou. |
| Timestamp | Yes | UInt | The current UNIX timestamp that records the time at which the API request was initiated. |
| Nonce | Yes | UInt | A random positive integer that is used in conjunction with Timestamp to prevent replay attacks. |
| SecretId | Yes | String | An ID that the user applies for on the [Cloud API Key](https://console.cloud.tencent.com/capi) for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request signature. For more information, see [Signature Method](https://cloud.tencent.com/document/api/377/4214). |
| Signature | Yes | String | Request signature, which is used to verify the validity of the request. It is generated based on input parameters. For more information, see [Signature Method](https://cloud.tencent.com/document/api/377/4214). |
| SignatureMethod | Yes | String | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. For more information, see [Signature Method](https://cloud.tencent.com/document/api/377/4214). |


**Example**

The following example shows how common request parameters look like in an API request link for a Tencent Cloud product. If, for example, you want to query the list of Tencent Cloud CVM instances in the Guangzhou region, the request link should look like this:
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

