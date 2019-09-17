## Format of Returned Results for Common Asynchronous Task APIs
Sending one request to general Asynchronous Task API allows you to operate only one type of resource at a time. For example, you can create load balancer or reset server operating system by making a call to the specified general Asynchronous Task API.
<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th><th> <b>Required</b>
</th></tr>
<tr>
<td> code
</td><td> Int
</td><td> Error code of the returned result. 0: success; other values: failure.
</td><td> Yes
</td></tr>
<tr>
<td> message
</td><td> String
</td><td> Error message of the returned result.
</td><td> No
</td></tr>
<tr>
<td> requestId
</td><td> String
</td><td> Task number
</td><td> Yes
</td></tr></tbody></table>

## Format of Returned Results for Batch Asynchronous Task APIs
With such asynchronous task APIs, multiple resources can be operated for each request, for example, changing passwords, starting or shutting down servers.
<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th><th> <b>Required</b>
</th></tr>
<tr>
<td> code
</td><td> Int
</td><td> Error code of the returned result. 0: success; other values: failure.
</td><td> Yes
</td></tr>
<tr>
<td> message
</td><td> String
</td><td> Error message of the returned result.
</td><td> No
</td></tr>
<tr>
<td> detail
</td><td> Array
</td><td> The code, message, and requestId of the resource operation are returned with the resource ID as the key.
</td><td> Yes
</td></tr></tbody></table>

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
		"qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0": {
			"code": 0,
			"message": "",
			"requestId": "1231231231232"
		}
	}
}
```
>!
>- If the operation succeeds for all resources, the outermost code is 0.
>- If the operation fails for all resources, the outermost code is 5100.
>- If the operation fails for some resources, the outermost code is 5400.
>- In the third case, the terminal can obtain information about the failed operations via the `detail` field.
