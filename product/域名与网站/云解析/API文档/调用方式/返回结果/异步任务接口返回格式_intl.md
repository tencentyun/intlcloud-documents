## Response Format for Ordinary Asynchronous Task APIs
One request can operate the asynchronous task API of one resource, such as creating load balancing or resetting the host operating system.
<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> code
</td><td> Int
</td><td> Error code of the response; 0 - success, other values - failure.
</td></tr>
<tr>
<td> message
</td><td> String
</td><td> Error message of the response.
</td></tr>
<tr>
<td> requestId
</td><td> String
</td><td> Task ID
</td></tr></tbody></table>

## Response Format for Batch Asynchronous Task APIs
One request can operate the asynchronous task APIs of multiple resources, such as changing a password, starting a server and stopping a server.
<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> code
</td><td> Int
</td><td> Error code of the response; 0 - success, other values - failure.
</td></tr>
<tr>
<td> message
</td><td> String
</td><td> Error message of the response.
</td></tr>
<tr>
<td> detail
</td><td> Array
</td><td> The code, message and requestId of the resource operation are returned with the resource ID as the key.
</td></tr></tbody></table>

For example:

```
{
        "code":0,
        "message": "success",
        "detail":
        {
             "qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0":
            {
             "code":0,
             "message":"",
             "requestId":"1231231231231":,
            }
              "qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0":
            {
              "code":0,
              "message":"",
              "requestId":"1231231231232":,
            }
        }
}
```
>**Note:**
If all the resources are successfully operated, the outermost code will be 0.
If all the resource operations failed, the outermost code will be 5100.
If some of the resource operations failed, the outermost code will be 5400.
In the third case, the terminal can get the operation information of the failed part in the detail.
