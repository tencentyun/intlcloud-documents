A complete TencentCloud API request consists of two types of parameters: common request parameters and API request parameters. This document describes API request parameters.
API request parameters vary by API. API request parameters should always begin with a lowercase letter so that they can be differentiated from common request parameters.

>! This document illustrates parameters specific to Tencent Cloud CVMs. For other Tencent Cloud services, see their API documentation for specific parameters.

The list below uses the DescribeInstances API as an example and contains its request parameters:

| Parameter | Description | Type | Required |
|---------|---------|---------|---------|
| instanceIds.n | Array of the IDs of CVM instances to query, with the array subscript starting from 0. You can use `instanceId` or `unInstanceId`, and we recommend using the uniform resource ID `unInstanceId`. | String | No |  
| lanIps.n | Array of private IPs of CVM instances to query. | String | No | 
| searchWord | User-defined CVM alias. | String | No |
| offset | The offset at which the entries start. The entry starts from 0. | Int | No |
| limit | The maximum number of instances that can be queried at a time. The default is 20 and the maximum is 100. | Int | No | 
| status | Status of the CVM to query. | Int | No |
| projectId | Project ID. CVM instances of all projects will be queried if this parameter is not passed in. The value `0` indicates the default project. If you want to query a specified project, call the DescribeProject API. | String | No |
| simplify | Non-real time data obtained if `simplify=1` is included in the input parameter| Int | No |
| zoneId | Availability zone ID. CVM instances in all availability zones will be queried if this parameter is not passed in. If you want to query a specified availability zone, call the [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API. | Int | No |

The above fields are described as follows:

**Parameter:** name of the request parameter supported by the API, which may be used in the API calling. A parameter name that ends with `.n` represents an array, for which you need to input the array parameters individually.
**Required:** indicates whether this parameter is required. "Yes" means the parameter is required for the API calling. "No" means the parameter can be left empty.
**Type:** data type of the API parameter.
**Description:** a brief description of the API request parameter.

### Example
The example shows you how to configure API request parameters for a TencentCloud API. For example, if you want to query the list of scaling groups for a Tencent Cloud CVM, use the following request link:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<<a href="https://intl.cloud.tencent.com/document/product/213/31574">Common request parameters</a>>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>
