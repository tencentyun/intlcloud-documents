

Asynchronous task API is not defined in the updated API documents (available for certain services only, such as CVM). For specific usage, see the `Action` field in each document.

## Response Format for Common Asynchronous Task APIs
Sending one request to common asynchronous task APIs allows you to operate only one type of resource at a time. For example, you can create CLB instance or reset the server’s operating system by making a call to the specified common asynchronous task API.

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
      <td>Error code of the returned result. 0: success; other values: failure.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message of the returned result.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>Task number.</td>
      <td>Yes</td>
   </tr>
</table>

## Response Format for Batch Asynchronous Task APIs
Sending one request to these asynchronous task APIs allows you to operate multiple resources. For example, you can change passwords, start or shut down servers.

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
      <td>Error code of the returned result. 0: success; other values: failure.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message of the returned result.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td>The code, message, and requestId of the resource operation are returned with the resource ID as the key.</td>
      <td>Yes</td>
   </tr>
</table>

Sample

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
>!
- If the operation succeeds for all resources, the outermost code is 0.
- If the operation fails for all resources, the outermost code is 5100.
- If the operation fails for some resources, the outermost code is 5400. In this case, the terminal can obtain information about the failed operations via the `detail` field.
