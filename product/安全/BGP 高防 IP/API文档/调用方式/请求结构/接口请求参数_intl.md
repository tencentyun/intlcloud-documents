A complete Tencent Cloud API request requires two types of request parameters: common request parameters and API request parameters. This document describes API request parameters that are used to specify which Tencent Cloud API is called. For information about common request parameters, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/377/4153).
API request parameters vary by API. The initial letter of each API request parameter should be in lowercase so that it can be differentiated from a common request parameter.
>**Note:**
>We take Tencent Cloud CVM-specific API as an example in this document. For other resource-specific APIs, please see relevant documents.

For example, the Tencent Cloud CVM API DescribeInstances has its specific parameters as the following table shown:

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| instanceIds.n | A array that contains the IDs of CVM instances you want to query with subscripts starting from 0. You can use either instanceId or unInstanceId. The unified resource ID unInstanceId is recommended. | String | No |  
| lanIps.n | Array of private IPs of the CVMs to be queried. | String | No | 
| searchWord | CVM alias set by the user. | String | No |
| offset | The value of offset. The default is 0. | Int | No |
| limit | The maximum number of servers that can be queried at a time. The defaul is 20. The maximum is 100. | Int | No | 
| status | Status of the CVM to be queried. | Int | No |
| projectId | Project ID. Query CVM instances of all projects if the parameter is null.| String | No |
| simplify | Return non-real time data when the input value is 1. | Int | No |
| zoneId | Availability zone ID. Query CVM instances in all availability zones if the parameter is null.  Call the API [DescribeAvailabilityZones](https://intl.cloud.tencent.com/document/api/213/15707) to get a list of availability zones. | Int | No |

The following describes the elements in a parameter:

**Parameter Name:** The name of the API-supported request parameter . You can use it as an API request parameter when calling the API.  `“.n”` at the end of a parameter name represents an array, which means that you need to input multiple parameter values.
**Required:**  Whether or not the parameter is required for the requests. "Yes" means you need to specify the parameter value. "No" means the input is optional.
**Type:** Data type of the parameter.
**Description:** A brief description of the parameter.

### Use Case
The following example shows how common request parameters are formatted in an Tencent Cloud API request when you want to query a list of scaling groups for a Tencent Cloud CVM:
<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<Common request parameters>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>


