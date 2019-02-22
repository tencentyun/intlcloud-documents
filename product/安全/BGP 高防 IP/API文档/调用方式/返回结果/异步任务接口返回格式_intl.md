[//]: # (chinagitpath:XXXXX)

The definitions of asynchronous task APIs are not provided in new API documents (available for partial services, such as CVM). For specific usage, see the Action field in each document.

## Format of Returned Results for Common Asynchronous Task APIs
With such asynchronous task APIs, only one resource can be operated for each request, for example, creating load balancer or resetting OS for server.

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
      <td>Error code on the result. 0: Successful; other values: Failed.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message on the result</td>
      <td>No</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>Task ID</td>
      <td>Yes</td>
   </tr>
</table>

## Format of Returned Results for Batch Asynchronous Task APIs
With such asynchronous task APIs, multiple resources can be operated for each request, for example, changing passwords, starting or shutting down servers.

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
      <td>Error code on the result. 0: Successful; other values: Failed.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message on the result</td>
      <td>No</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td>The code, message, and requestId returned for an operation performed on the resource with the resource ID as key.</td>
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
		}
	}
}
```
>!
>- If the operations are successful for all resources, the outermost code is 0.
>- If the operations fail for all resources, the outermost code returns 5100.
>- If the operations fail for some resources, the outermost code returns 5400. In this case, the terminal can obtain the information about the failed operations via the "detail" field.

