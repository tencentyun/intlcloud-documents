>**This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using [CVM API v3.0], which is more standardized and has much lower access latency [API Category](https://intl.cloud.tencent.com/document/api/213/15689).**
>

Asynchronous task API is not defined in the updated API documents (available for certain services only, such as CVM). For specific usage, see the `Action` field in each document.

## Format of Returned Results for Common Asynchronous Task APIs
Sending one request to general asynchronous task APIs allows you to operate only one type of resource at a time. For example, you can create load balancer or reset the server’s operating system by making a call to the specified general asynchronous task API.

<table>
   <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>Error code of the returned result. 0: success; other values: failure</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message of the returned result</td>
      <td>No</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>Task number</td>
      <td>Yes</td>
   </tr>
</table>

## Format of Returned Results for Batch Asynchronous Task APIs
With such asynchronous task APIs, multiple resources can be operated for each request. For example, you can change passwords, start or shut down servers.

<table>
   <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>Error code of the returned result. 0: success; other values: failure</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message of the returned result</td>
      <td>No</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td>The code, message and requestId of the resource operation are returned with the resource ID as the key</td>
      <td>Yes</td>
   </tr>
</table>

For example:

```
{
	"code": 0,
	"message": "success",
	"detail": {
		"qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0": {
			"code": 0,
			"message": "",
			"requestId": "1231231231231"
		},
		"qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc1": {
			"code": 0,
			"message": "",
			"requestId": "1231231231232"
		}
	}
}
```
>
>- If the operation succeeds for all resources, the outermost code is 0.
>- If the operation fails for all resources, the outermost code is 5100.
>- If the operation fails for some resources, the outermost code is 5400. In this case, the terminal can obtain information about the failed operations via the `detail` field.
