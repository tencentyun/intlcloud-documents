>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>

>**This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using [API Category](https://intl.cloud.tencent.com/document/api/213/15689), which is more standardized and has much lower access latency see [API Category](https://intl.cloud.tencent.com/document/api/213/15689).**
>

A complete TencentCloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes the six common request parameters required by TencentCloud API requests. For detailed descriptions of API request parameters, see [API Request Parameters](https://intl.cloud.tencent.com/document/product/597/10085).
Common request parameters are required in every API. When using TencentCloud APIs to send requests, make sure that the common request parameters are passed in; otherwise, the requests will fail. Common request parameters should always begin with a capital letter so that they can be differentiated from API request parameters.

The following lists the specific common request parameters:
>**Note:**
>This document illustrates APIs specific to Tencent Cloud CVMs. For APIs specific to other Tencent Cloud products, see the relevant documents.

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| Action | Name of an action-specific API. For example, when a Tencent Cloud CVM user calls the API [Querying Instance List](https://intl.cloud.tencent.com/document/api/213/9388), the Action parameter is DescribeInstances | String | Yes |
| Region | The Region parameter, which is used to identify the region of the instance you want to work with. For more information, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091) or call the [Querying Region List] API (https://intl.cloud.tencent.com/document/api/213/9456). <br>**Note:** 1. Unless otherwise specified in the API document, this parameter is required. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2. Certain regions are currently in beta and only available to allowlisted users | String | No |
| Timestamp | The current UNIX timestamp that records the time when the API request is initiated | UInt | Yes |
| Nonce | The user-defined random positive integer, which is used in conjunction with Timestamp to prevent replay attacks | UInt | Yes |
| SecretId | An ID that the user applies for on the [TencentCloud API Key](https://console.cloud.tencent.com/capi) page for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request signature (Signature). For more information, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693) | String | Yes |
| Signature | The request signature, which is used to verify the validity of the request. It is generated based on the actual input parameters. For the calculation method, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693) | String | Yes |
| SignatureMethod | Signature method. Supported methods are HmacSHA256 and HmacSHA1. The HmacSHA256 method is used to verify signatures only when the parameter is specified as HmacSHA256. Otherwise, HmacSHA1 is used. For more information, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693) | String | No |
| Token | The token used by the temporary certificate, which needs to be used in conjunction with the temporary key. No token is required for permanent keys | String | No |

### Use Cases
The following examples show how a common request parameter looks like in a TencentCloud API request. For example, if you want to query the list of Tencent Cloud CVM instances in Guangzhou region, the desired request format is:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<<a href="https://intl.cloud.tencent.com/document/product/597/10085">API-specific Request Parameters</a>>
</pre>
