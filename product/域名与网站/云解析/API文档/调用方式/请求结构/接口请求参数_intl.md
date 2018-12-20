A complete Tencent Cloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes the API request parameters that Tencent Cloud API requests need. For a detailed description of the common request parameters, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153).
API request parameters depend on specific APIs, and the API request parameters supported by different APIs are different. The first letter of an API request parameter is always lowercase, which is to distinguish it from a common request parameter.
>**Note:**
>The parameters in this document use Tencent Cloud CVM as an example. For the actual parameters of each Tencent Cloud product, see the actual product's API parameter description.

The following parameter list uses Tencent Cloud CVM's [instance list-querying](https://intl.cloud.tencent.com/document/api/213/831) API (DescribeInstances) as an example. This API supports the following API request parameters:

| Parameter name | Description | Type | Required |
|---------|---------|---------|---------|
| instanceIds.n | Array of the CVM instance ID to be queried; the array subscript starts at 0. You can use instanceId and unInstanceId, and it is recommended to use the uniform resource ID: unInstanceId. | String | No |
| lanIps.n | Array of the private IP of the CVM instance to be queried. | String | No |
| searchWord | User-defined host alias. | String | No |
| offset | Offset, 0 by default. | Int | No |
| limit | The maximum number of instances that can be queried at a time. The default is 20 and the maximum is 100. | Int | No |
| status | The status of the host to be queried. | Int | No |
| projectId | Project ID; if not passed in, the CVM instances of all projects will be queried. 0 indicates the default project. If you need to specify other projects, you can call the project list-querying API (DescribeProject) to query. | String | No |
| simplify | Get non-real-time data; if simplify=1 is added to the parameter passed in, the non-real-time data will be obtained. | Int | No |
| zoneId | Availability zone ID. If not passed in, the CVM instances of all availability zones will be queried. To specify the availability zone, you can call the [availability zone-querying](https://intl.cloud.tencent.com/document/api/213/1286) API (DescribeAvailabilityZones) to query. | Int | No |

The description of each field is as follows:

**Parameter name:** The name of the request parameter supported by this API. You can use it as API request parameter when using this API. If the parameter name ends in `.n`, it means that this parameter is an array, and you need to pass in the array parameters in turn when using it.
**Required:** This indicates whether this parameter is required. If it is "yes", it means that this parameter must be passed in when calling this API; if it is "no", this parameter can be ignored.
** Type:** The data type of this API parameter.
** Description:** This briefly describes the content of this API request parameter.

### Usage Examples
In the API request links of Tencent Cloud products, the API request parameters are in the following form. With Tencent Cloud CVM as an example, if you want to query the scaling group list, the form of the request link is as below:

<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<<a href="https://intl.cloud.tencent.com/document/api/229/6976">Common request parameter</a>>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>

