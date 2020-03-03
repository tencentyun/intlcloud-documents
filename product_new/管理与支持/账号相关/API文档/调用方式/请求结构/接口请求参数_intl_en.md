API request parameters vary by API. API request parameters should always begin with a lowercase letter so that they can be differentiated from common request parameters.
For example, the <a href="https://intl.cloud.tencent.com/document/product/378/4398" title="AddProject">AddProject</a> API supports the following API request parameters:

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| projectName  | Yes | String |  Project name containing Chinese and English characters as well as digits. |
| projectDesc | No | String | Project description. |


The descriptions of each field are as follows:
<table class="t">
<tbody>
<td> Parameter Name
</td><td> Name of the request parameter supported by the API. You can use it as an API request parameter when using the API.<br>
</td></tr>
<tr>
<td> Required
</td><td> Indicates whether this parameter is required. "Yes" means that the parameter is required for the API, while "No" means that it is optional.
</td></tr>
<tr>
<td> Type
</td><td> Data type of this API parameter.
</td></tr>
<tr>
<td> Description
</td><td> A brief description of the API request parameter.
</td></tr>
</tbody></table>

Suppose you want to query a created project, a sample of the request would be as follows:

<pre>
  https://account.api.qcloud.com/v2/index.php?Action=AddProject
  &<a href="https://intl.cloud.tencent.com/document/product/378/4380">Common request parameters</a>
  &projectName=test
  &projectDesc=For testing
</pre>

A complete TencentCloud API request requires two types of parameters: common request parameters and API request parameters. This document only describes API request parameters. For more information on common request parameters, please see <a href="https://intl.cloud.tencent.com/document/product/378/4380" title="Common Request Parameters">Common Request Parameters</a>.
