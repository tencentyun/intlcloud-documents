A complete Tencent Cloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes the six common request parameters that Tencent Cloud API requests need.
Common request parameters are the ones that each API needs to use. Each time the developer sends a request using the Tencent Cloud API, the common request parameters need to be carried; otherwise, the request will fail. The first letter of a common request parameter is always uppercase, which is to distinguish it from an API request parameter.

Below lists the specific common request parameters:
>**Note:**
>The API instances in this document use Tencent Cloud CVM as an example. For the actual usage of each Tencent Cloud product, see the actual product's documentation.

| Parameter name | Description | Type | Required |
|---------|---------|---------|---------|
| Action | The name of the command API for the specific operation. For example, if you want to call the [instance list-querying](https://intl.cloud.tencent.com/document/api/213/9388) API of CVM, then the Action parameter is DescribeInstances. | String | Yes |
| Region | The Region parameter used to identify the region whose instance you want to operate on. For more information, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091) or use the [region list-querying](https://intl.cloud.tencent.com/document/api/213/9456) API to view. <br>**Note:** 1. This parameter is required under normal circumstances. If it is not required to be passed in, this will be stated in the corresponding API. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. Some regions are currently in trial and only available to selected users. | String | No |
| Timestamp | The current UNIX timestamp which records when an API request is initiated. | UInt | Yes |
| Nonce | A random positive integer used to prevent replay attacks along with Timestamp. | UInt | Yes |
| SecretId | The SecretId for identification obtained on the [Cloud API Key](https://console.cloud.tencent.com/capi) page. A SecretId corresponds to a unique SecretKey which is used to generate the request signature (Signature). For details, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693). | String | Yes |
| Signature | Request signature used to verify the validity of this request. This is generated based on the actual input parameters. For calculation method, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693). | String | Yes |
| SignatureMethod | Signature method. Currently, only HmacSHA256 and HmacSHA1 are supported. The HmacSHA256 algorithm is used to verify the signature only when this parameter is specified as HmacSHA256. In other cases, the signature is verified with HmacSHA1. For detailed signature calculation method, see [Signature Method](https://intl.cloud.tencent.com/document/product/215/1693). | String | No |
| Token | The token used by the temporary certificate, which needs to be used in conjunction with the temporary key. Long-term keys do not require a token. | String | No |

### Usage Examples
In the API request links of Tencent Cloud products, the common request parameters are in the following form. With Tencent Cloud CVM as an example, if you want to query the CVM instance list in the Guangzhou region, the form of the request link is as below:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<<a href="https://cloud.tencent.com/document/api/377/4154">API request parameter</a>>
</pre>


