[//]: # (chinagitpath:XXXXX)

A complete Tencent Cloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes 6 common request parameters used in Tencent Cloud API requests. For more information about API request parameters, see [API Request Parameters](https://cloud.tencent.com/document/product/1014/31225).
Common request parameters are required in every API. When you send requests to Tencent Cloud APIs, please make sure that the requests include ooth common request parameters and API request parameters. Otherwise, the requests will fail. Also, you need to capitalize the first letter in each common request parameter so that it can be differentiated from a API request parameter.

Common request parameters are shown in the following table:
>**Note:**
>We take Tencent Cloud CVM-specific API as an example in this document. For other resource-specific APIs, please see relevant documents.

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| Action | Name of an action-specific API. For example, when a Tencent Cloud CVM user calls the API [DescribeInstance](https://cloud.tencent.com/document/api/213/9388), the **Action** of this request is DescribeInstances. | String | Yes |
| Region | Name of the region where your desired instance is located. For more information, see [Regions and Availability Zones](https://cloud.tencent.com/document/product/213/6091), or use the API [DescribeRegions](https://cloud.tencent.com/document/api/213/9456).<br> **Notes:** 1. This parameter is required for the API requests, unless otherwise specified.<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. The product is in closed beta in some of the regions and not available to all users. | String | No |
| Timestamp | Current UNIX timestamp, which is the time when the API request was initiated. | UInt | Yes |
| Nonce | A random positive integer that is combined with Timestamp to prevent replay attacks. | UInt | Yes |
| SecretId | Identity of the Tencent Cloud API access key Applicant [Cloud API Key](https://console.cloud.tencent.com/capi). A SecretId corresponds to one unique SecretKey, which is used to generate a request Signature. For more information, see [Signature Method](https://cloud.tencent.com/document/product/215/1693). | String | Yes |
| Signature | A signature is used for adding authentication information to the requests so that Tencent Cloud APIs can validate the identity of the request. The creation of signatures is based on input parameters. For more information, see [Signature Method](https://cloud.tencent.com/document/product/215/1693). | String | Yes |
| SignatureMethod | Types of message authentication methods. HmacSHA256 and HmacSHA1 are supported. If HmacSHA256 is not specified, the default is HmacSHA1. For more information, see [Signature Method](https://cloud.tencent.com/document/product/215/1693). | String | No |
| Token | No | A token must be included in an API call along with temporary credentials.  Long-term credentials do not require tokens. | String | No |

### Use Case
The following example shows how common request parameters are formatted in an Tencent Cloud API request when you want to query the list of Tencent Cloud CVM instances in the Guangzhou region:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<API request parameters>
</pre>



