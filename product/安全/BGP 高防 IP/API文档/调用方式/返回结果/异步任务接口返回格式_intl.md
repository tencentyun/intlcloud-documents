[//]: # (chinagitpath:XXXXX)

Asynchronous task API is not defined in updated API and currently only partial products and services such as CVM are available. For specific usage, see *Action* documentations.

## General Asynchronous Task API Result 
Sending one request to general Asynchronous Task API allows you to operate only one type of resource at a time. For example, you can create load balancer or reset server operating system by making a call to the specified general Asynchronous Task API.
**Format**
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
      <td>Error code. 0: Successful; other values: Failed.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message</td>
      <td>No</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>Task ID</td>
      <td>Yes</td>
   </tr>
</table>

## Asynchronous Task-Chain API 
Sending one request to Asynchronous Task-Chain API allows you to operate multiple types of resources at a time. For example, you can change passwords and start/shutt down servers at the same time by making a call to the specified Asynchronous Task-Chain API. 

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
      <td>Error code. 0: Successful; other values: Failed.</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>Error message</td>
      <td>No</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td> Details of the operation: code, message, and requestId. Key is resource ID</td>
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
>- If you successfully operate all resources, the "code" in the first layer is 0.
>- If you fail to operate all resources, the "code" in the first layer is 5100.
>- If you fail to operate some resources, the outermost code returns 5400. In this case, you can find the detailed information in "detail" in the result.

