If an error code is returned after the function is executed, you can find the cause and solution by referring to the following table.



<table>
<thead>
<tr>
<th>Status Code and Status Message</th>
<th>Description</th>
<th>Solution</th>
</tr>
</thead>
<tbody>

<tr>
<td>200<br>Success</td>
<td>The execution is successful.</td>
<td>-</td>
</tr>

<tr>
<td>400<br>BadRequest</td>
<td>The input parameters are incorrect.</td>
<td><ul class="params"><li>Check whether the input parameters are correct based on the error message.</li>
<li>The parameters are invalid. Please revise the parameters by referring to <a href="https://intl.cloud.tencent.com/document/product/583/17234" target="_blank">API Documentation</a> and retry.</li></ul></td>
</tr>

<tr>
<td>401<br>InvalidCredentials</td>
<td>The verification fails.</td>
<td>-</td>
</tr>

<tr>
<td>403<br>ResourceUnavailable</td>
<td>The resource is unavailable.</td>
<td>-</td>
</tr>

<tr>
<td>404<br>InvalidSubnetID</td>
<td>The subnet ID is invalid.</td>
<td>Check whether the <a href="https://intl.cloud.tencent.com/document/product/583/38377" target="_blank" rel="noopener noreferrer">Network configuration</a> of the function is correct and whether the subnet ID is valid.</td>
</tr>

<tr>
<td>406<br>RequestTooLarge</td>
<td>The request body size is too large.</td>
<td><ul class="params"><li>Reduce the request body size based on the product documentation.</li>
<li>Based on the request body size, determine whether the parameter value is too large. For sync requests, the limit is 6 MB; for async requests, the limit is 128 KB.</li></ul></td>
</tr>

<tr>
<td>430<br>UserFunctionExecError</td>
<td>User code execution error occurs.</td>
<td>Based on the error log on the Console, check the error stack of code and see whether the code can be executed properly.</td>
</tr>

<tr>
<td>432<br>ResourceLimitReached</td>
<td>The concurrence limit is reached.</td>
<td>You can <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">submit a ticket</a> to increase the concurrence limit.</td>
</tr>

<tr>
<td>433<br>TimeLimitReached</td>
<td>Function execution timed out.</td>
<td><ul class="params"><li>Check whether a large number of time-consuming operations exist in the service code.</li>
<li>Set a longer timeout period. If the current timeout period has been set to the maximum value, you can <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">submit a ticket</a> to increase the timeout limit.</li></ul></td>
</tr>

<tr>
<td>434<br>MemoryLimitReached </td>
<td>The memory limit is reached.</td>
<td><ul class="params"><li>Set a larger memory size on the "Function configuration" page. If the current memory size has been set to the maximum value, you can <a href="https://console.cloud.tencent.com/workorder/category" target="_blank" rel="noopener noreferrer">submit a ticket</a> to increase the memory limit.</li>
<li>Check the code logic to see if memory leak exists.</li></ul></td>
</tr>

<tr>
<td>435<br>FunctionNotFound</td>
<td>The function is not found.</td>
<td>Check whether the function is deleted, or whether the function information that is used as the input parameter is correct.</td>
</tr>

<tr>
<td>436<br>InvalidParameterValue</td>
<td>The parameter is invalid.</td>
<td>-</td>
</tr>

<tr>
<td>437<br>HandlerNotFound</td>
<td>The function package is loaded incorrectly.</td>
<td>Check whether the handler is correctly configured. For more information, please see <a href="#handler">Execution Method</a>.</td>
</tr>

<tr>
<td>438<br>FunctionStatusError</td>
<td>SCF service is suspended because the Tencent Cloud account is in arrears.</td>
<td>-</td>
</tr>

<tr>
<td>439<br>UserProcExitError</td>
<td>User process exists accidentally.</td>
<td>Based on the error message, find out the cause and fix the function code.</td>
</tr>

<tr>
<td>441<br>UnauthorizedOperation</td>
<td>CAM authentication fails.</td>
<td>The request is unauthorized. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/598" target="_blank">Cloud Access Management</a>.</td>
</tr>

<tr>
<td>442<br>QualifierNotFound</td>
<td>The specified version is not found.</td>
<td>The function version does not exist. Please check the function version and retry.</td>
</tr>

<tr>
<td>500<br>InternalError</td>
<td>Internal error occurs.</td>
<td>-</td>
</tr>

<tr>
<td>532<br>ResourceExhausted</td>
<td>Computing resources are insufficient.</td>
<td>-</td>
</tr>

</tbody>
</table>

<style>
.params{margin:0px !important}
</style>


## Concepts
#### Execution method<div id="handler"></div>
Execution method specifies which function in which file is executed first when the cloud function is invoked, as shown in the following figure.
![](https://main.qcloudimg.com/raw/48172f9407d4002f79ad0355e609aff2.png)
- For Golang programming, use the **FileName** format, for example, `main`.
- For Python, Node.js, or PHP programming, use the **FileName.FunctionName** format, for example, `index.main_handler`.
	- Please note that **FileName does not include the file name extension, and FunctionName is the name of the entry function.** Ensure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`; and for Node.js programming, the file name extension is `.js`. For more information, please see [Execution Method](https://intl.cloud.tencent.com/document/product/583/9210). 
- For Java programming, use the **package.class::method** format, for example, `example.Hello::mainHandler`.
- For the Custom Runtime environment, a non-fixed format can be used based on the custom programming language implementation.

         
