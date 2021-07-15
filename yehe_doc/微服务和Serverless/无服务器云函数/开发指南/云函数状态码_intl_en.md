If an error code is returned after the function is executed, you can find the cause and solution for the error code by referring to the following table.


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
<td>400<br>InvalidParameterValue</td>
<td>The input parameters are incorrect.</td>
<td>The parameter does not conform to the specification. Please modify it as instructed in <a href="https://intl.cloud.tencent.com/document/product/583/17234">Introduction</a> and try again.</td>
</tr>
<tr>
<td>401<br>InvalidCredentials</td>
<td>The verification fails.</td>
<td>The verification fails. Your account does not have the permission to manipulate this function. Please check the permission and try again. For more information, please see the authorization description in <a href="https://intl.cloud.tencent.com/document/product/583/18014" >Permission Management Overview</a>.</td>
</tr>
<tr>
<td>404<br>InvalidSubnetID</td>
<td>The subnet ID is invalid.</td>
<td>Check whether the <a href="https://intl.cloud.tencent.com/document/product/583/38377">network configuration</a> of the function is correct and whether the subnet ID is valid.</td>
</tr>
<tr>
<td>405<br>ContainerStateExited	</td>
<td>The container exits.</td>
<td>Please check your image or bootstrap file to see whether it can be properly started locally.</td>
</tr>
<tr>
<td>406<br>RequestTooLarge</td>
<td>The request body size is too large.</td>
<td>The request event size exceeds the upper limit, which is 6 MB for sync request events or 128 KB for async ones.</td>
</tr>
<tr>
<td>407<br>The size of response exceeds the upper limit (6MB)</td>
<td>The size of function response exceeds the upper limit of 6 MB.</td>
<td>The size of function response exceeds the upper limit of 6 MB. Please adjust it and try again.</td>
</tr>
<tr>
<td>410<br>InsufficientBalance</td>
<td>The account balance is insufficient.</td>
<td>The SCF service is suspended because the Tencent Cloud account has overdue payments. Please top up and try again.</td>
</tr>
<tr>
<td>429<br>ResourceLimit</td>
<td>The container request rate is too high.</td>
<td>The container request rate is too high. Please try again later.</td>
</tr>
<tr>
<td>430<br>User code exception caught</td>
<td>A user code execution error occurs.</td>
<td>Based on the error log on the console, check the error stack of the code and see whether the code can be executed properly.</td>
</tr>
<tr>
<td>432<br>ResourceLimitReached</td>
<td>The concurrency limit is reached.</td>
<td>Container resource usage exceeds the upper limit (the number of concurrent functions * 2). Please adjust the code or <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to increase the function concurrency limit.</td>
</tr>
<tr>
<td>433<br>TimeLimitReached</td>
<td>The function execution times out.</td>
<td><ul class="params"><li>Check whether a large number of time-consuming operations exists in the service code.</li>
<li>Set a longer timeout period on the **FUNCTION Configuration** page. If the current timeout period has been set to the maximum value, you can <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to increase the timeout limit.</li></ul></td>
</tr>
<tr>
<td>434<br>MemoryLimitReached </td>
<td>The memory limit is reached.</td>
<td><ul class="params"><li>Check the code logic to see whether there is a memory leak.</li>
<li>Set a larger memory size on the **Function Configuration** page. If the current memory size has been set to the maximum value, you can <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to increase the memory limit.</li></ul></td>
</tr>
<tr>
<td>435<br>FunctionNotFound</td>
<td>The function is not found.</td>
<td>Check whether the function is deleted or whether the function information that is used as the input parameter is correct.</td>
</tr>
<tr>
<td>436<br>InvalidParameterValue</td>
<td>The parameter is invalid.</td>
<td>The parameter does not conform to the specification. Please modify it as instructed in <a href="https://intl.cloud.tencent.com/document/product/583/17234">Introduction</a> and try again.</td>
</tr>
<tr>
<td>437<br>HandlerNotFound</td>
<td>The function package is loaded incorrectly.</td>
<td>The function entry file is not found. Please check whether the entry file name in the code package matches the handler settings and whether the code package is normal. For more information on the handler, please see <a href="#handler">Execution method</a>.</td>
</tr>
<tr>
<td>438<br>FunctionStatusError</td>
<td>The function is exceptional or the SCF service is suspended.</td>
<td><ul class="params"><li>The function is invoked in an exceptional state. Please wait for the function status to become normal and try again.</li>
	<li>The SCF service is suspended because the Tencent Cloud account has overdue payments. Please top up and try again.</li></ul></td>
</tr>
<tr>
<td>439<br>User preocess exit when running</td>
<td>The user process exits accidentally.</td>
<td>Based on the error message, find out the cause and fix the function code.</td>
</tr>
<tr>
<td>440<br>BorrowContainerDegrade</td>
<td>The borrowed container circuit breaker is triggered.</td>
<td>The borrowed container circuit breaker is triggered. This may be because that the expansion speed or concurrency exceeds the limit. Please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to increase the expansion speed or <a href="https://intl.cloud.tencent.com/document/product/583/37040">concurrency quota</a>.</td>
</tr>
<tr>
<td>441<br>UnauthorizedOperation</td>
<td>CAM authentication fails.</td>
<td>Check whether the CAM authentication parameters for the function invoker are passed correctly. For more information, please see the authorization description in <a href="https://intl.cloud.tencent.com/document/product/583/18014" >Permission Management Overview</a>.</td>
</tr>
<tr>
<td>442<br>QualifierNotFound</td>
<td>The specified version is not found.</td>
<td>The function version does not exist. Please check the function version and try again.</td>
</tr>
<tr>
<td>443<br>UserCodeError</td>
<td>A user code execution error occurs.</td>
<td>Based on the error log on the console, check the error stack of the code and see whether the code can be executed properly.</td>
</tr>	
<tr>
<td>444<br>PullImageFailed</td>
<td>Image pull fails.</td>
<td>Please check the integrity and validity of the selected image and try again; for example, check whether it can be downloaded locally. If the problem persists, please <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</td>
</tr>
<tr>
<td>445<br>ContainerInitError</td>
<td>Container start fails.</td>
<td>Container start fails. Please check whether your bootstrap file has been uploaded successfully and ensure that the invocation path is correct.</td>
</tr>	
<tr>
<td>446<br>PortBindingFailed</td>
<td>Port listening fails.</td>
<td>The initialization of the container exceeds the maximum time of 30s. Please check whether the listening port is <code>9000</code>.</td>
</tr>
<tr>
<td>447<br>PullImageTimeOut</td>
<td>Image pull times out.</td>
<td>It may be a timeout caused by a large image or network jitters. Please minimize the image and try again. If the problem persists, please <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">submit a ticket</a>.</td>
</tr>
<td>450<br>InitContainerTimeout</td>
<td>The user code container times out.</td>
<td>The user code container times out (15s). Please check the code and try again. If the problem persists, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
<tr>
<td>449<br>InsufficientResources</td>
<td>The memory resources are insufficient.</td>
<td>The memory resources are insufficient. Please try again later.</td>
</tr>
<tr>
<td>500<br>InternalError</td>
<td>An internal error occurs.</td>
<td>An internal error occurs. Please try again later. If the problem persists, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
</tbody>
</table>

<style>
.params{margin:0px !important}
</style>

## Concepts
#### Execution method

The execution method specifies the starting file and function while invoking the cloud function as shown below:
![](https://main.qcloudimg.com/raw/81835da7292ef575fde6d634a99bb1e5.png)

- For Go programming, use the **FileName** format, such as `main`.
- For Python, Node.js, or PHP programming, use the **FileName.FunctionName** format, such as `index.main_handler`.
	
	- Please note that **FileName does not include the file name extension, and FunctionName is the name of the entry function.** Ensure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`, and for Node.js programming, the file name extension is `.js`. For more information, please see "Execution Method" in [Basic Concepts](https://intl.cloud.tencent.com/document/product/583/9210). 
- For Java programming, use the **package.class::method** format, such as `example.Hello::mainHandler`.
- For the Custom Runtime environment, a non-fixed format can be used based on the custom programming language implementation.

  ​       
