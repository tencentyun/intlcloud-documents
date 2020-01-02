A complete TencentCloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes the API request parameters required by TencentCloud API requests. For detailed descriptions of common request parameters, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/628/18814).
API request parameters vary by API. API request parameters should always begin with a lowercase letter so that they can be differentiated from common request parameters.

>This document illustrates parameters specific to Tencent Cloud CVMs. For parameters specific to other Tencent Cloud products, see the relevant API documents.

For example, the Tencent Cloud CVM API [Querying Instance List](https://intl.cloud.tencent.com/document/product/213/15728) (DescribeInstances) supports the following API request parameters:

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| instanceIds.n | The array of the IDs of the CVM instances to be queried, with the array subscript starting at 0. You can use `instanceId` and `unInstanceId`, and we recommend using the uniform resource ID `unInstanceId`. | String | No |
| lanIps.n | The array of the private IPs of the CVM instances to be queried. | String | No |
| searchWord | The user-defined CVM instance alias. | String | No |
| offset | The offset at which the entries start. The first entry is 0, the second entry is 1, and so on and so forth. | Int | No |
| limit | The maximum number of instances that can be queried at a time. The default is 20 and the maximum is 100. | Int | No |
| status | The status of the CVM instance to be queried. | Int | No |
| projectId | The ID of the project. If this parameter is not passed in, the CVM instances of all projects will be queried. 0 indicates the default project. If you want to specify other projects, call the Query Project List API (DescribeProject) to query. | String | No |
| simplify | Obtains non-real time data if the input parameter `simplify=1` is passed in. | Int | No |
| zoneId | The ID of the availability zone. If this parameter is not passed in, the CVM instances in all availability zones will be queried. If you want to specify an availability zone, call the Query Availability Zone List API (DescribeAvailabilityZones) to query. | Int | No |

The descriptions of each field are as follows:

**Parameter Name:** The name of the request parameter supported by the API. You can use it as an API request parameter when calling the API. A parameter name ending with `".n" ` represents an array, for which you need to pass in the array members individually.
**Required:** Indicates whether this parameter is required. "Yes" means the parameter is required when you call the API. "No" means the parameter can be left empty.
**Type:** Data type of the API parameter.
**Description:** A brief description of the API request parameter.

### Use Cases
The following sample shows how API request parameters look in a TencentCloud API request. For example, if you want to query the list of scaling groups for a Tencent Cloud CVM, the request link should look like this:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<<a href="https://intl.cloud.tencent.com/document/api/302/7302">Common Request Parameter</a>>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>

