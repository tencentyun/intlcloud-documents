If an error code is returned after the function is executed, you can find the cause and solution for the error code by referring to the following table.

<table>
<thead>
<tr>
<th>Status Code and Status Message</th>
<th>Description</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>200<br>Success</td>
<td>The execution is successful.</td>
<td>-</td>
</tr><tr>
<td>400<br>InvalidParameterValue</td>
<td>The request event passed in by the event execution function is not of the JSON type.</td>
<td>Make modifications as instructed in <a href="https://intl.cloud.tencent.com/document/product/583/17234">Introduction</a> and <a href="https://intl.cloud.tencent.com/document/product/583/41408">InvokeFunction</a> and try again.</td>
</tr><tr>
<td>401<br>InvalidCredentials</td>
<td>The verification fails.</td>
<td>Your account does not have the permission to manipulate this function. Make modifications as instructed in the authorization description in <a href="https://intl.cloud.tencent.com/document/product/583/18014" >Permission Management Overview</a> and try again.</td>
</tr><tr>
<td>402<br>ServiceSuspended</td>
<td>The service is temporarily suspended.</td>
<td>Your SCF service is temporarily suspended. You can refer to <a href="https://intl.cloud.tencent.com/document/product/583/12283" >Service Resumption</a> to make changes and try again later.</td>
</tr>	<tr>
<td>404<br>InvalidSubnetID</td>
<td>The subnet ID in the network configuration of the function is abnormal.</td>
<td>Check whether the <a href="https://intl.cloud.tencent.com/document/product/583/38377">network configuration</a> of the function is correct and whether the subnet ID is valid.</td>
</tr><tr>
<td>405<br>ContainerStateExited	</td>
<td>The container exits.</td>
<td>Check your image or bootstrap file to see whether it can be properly started locally.<br>If so, check whether the use limits of SCF are followed; for example, RootFS is read-only and only `/tmp` is writable.
<br>Local debugging command: `docker run -itd --read-only -v /tmp:/tmp`.</td>
</tr><tr>
<td>406<br>RequestTooLarge</td>
<td>The `event` input parameter of the function, i.e., the request event size of the function, exceeds the <a href="https://intl.cloud.tencent.com/document/product/583/11637">quota limit</a>.</td>
<td>The request event size exceeds the quota limit, which is 6 MB for sync request events or 128 KB for async ones. Adjust the request event size accordingly and try again.</td>
</tr><tr>
<td>407<br>The size of response exceeds the upper limit (6MB)</td>
<td>The size of function response exceeds the upper limit of 6 MB.</td>
<td>Adjust it and try again.</td>
</tr><tr>
<td>410<br>InsufficientBalance</td>
<td>The account balance is insufficient.</td>
<td>The SCF service is suspended because the Tencent Cloud account has overdue payments. Top up and try again.</td>
</tr><tr>
<td>429<br>ResourceLimit</td>
<td>The container request rate is too high and exceeds the limit due to concurrency surges.</td>
<td>The default upper speed of elastic concurrency expansion (function burst) for each account is 500 concurrent instances per region per minute. During a sudden concurrency surge, if there are not enough containers to carry the requests, a large number of container request actions will be triggered, and this message will be returned when the account limit is exceeded.<ul class="params"><li>After assessing the function concurrency, configure <a href="https://intl.cloud.tencent.com/document/product/583/37040">provisioned concurrency</a> for the function and prepare containers in advance to avoid sudden concurrency surges from causing the container request speed to exceed the limit.</li>
<li>If assessment shows that the provisioned concurrency cannot meet the needs of your business scenario, you can purchase a <a href="https://console.cloud.tencent.com/scf/buy?rid=1&ns=default">function package</a> to increase the function burst in the region.</td>
</tr><tr>
<td>430<br>User code exception caught</td>
<td>A user code execution error occurs.</td>
<td>Check the code error stack information in the invocation log provided by the SCF console, make modifications, and try again.</td>
</tr><tr>
<td>432<br>ResourceLimitReached</td>
<td>The account-level or region-level concurrency limit is reached.</td>
<td><ul class="params"><li>For a function with a reserved quota configured, if the function concurrency exceeds the quota, `Function [ xxx ] concurrency exceeded reserved quota xxx MB` will be returned. You can assess your business needs and increase the quota or refer to <a href="https://intl.cloud.tencent.com/document/product/583/39848">Concurrency Overrun Troubleshooting</a>.</li>
<li>For a function with no reserved quota configured, if the concurrency quota actually used by the function exceeds the region-level unused concurrency quota, `Function [ xxx ] concurrency exceeded region unreserved quota xxx MB` will be returned. You can assess your business needs and configure a reserved quota for the function. If the remaining available quota in the corresponding region cannot meet your business needs, you can purchase a <a href="https://console.cloud.tencent.com/scf/buy?rid=1&ns=default">function package</a> to increase the total concurrency quota in the region.</td>
</tr><tr>
<td>433<br>TimeLimitReached</td>
<td>Function execution is not completed after the <a href="https://intl.cloud.tencent.com/document/product/583/19805">execution timeout period</a> elapses.</td>
<td><ul class="params"><li>Check whether a large number of time-consuming operations exist in the service code.</li>
<li>Set a longer timeout period on the **Function configuration** page. If the current timeout period has been set to the maximum value, you can create an async function as instructed in <a href="https://intl.cloud.tencent.com/document/product/583/39466">Async Execution</a> to get a function execution duration of up to 24 hours.</li><li>This status code will trigger <a href="https://intl.cloud.tencent.com/document/product/583/37040#.E5.B9.B6.E5.8F.91.E5.AE.9E.E4.BE.8B.E5.A4.8D.E7.94.A8.E4.B8.8E.E5.9B.9E.E6.94.B6">instance repossession</a>.</li></ul></td>
</tr><tr>
<td>434<br>MemoryLimitReached </td>
<td>The memory limit is reached.</td>
<td><ul class="params"><li>Check the code logic to see whether there is a memory leak.</li>
<li>Increase the memory configuration on the **Function Configuration** page, or apply for a large memory on the **Function Memory Configuration** page to get up to 120 GB of function execution memory.</li><li>This status code will trigger <a href="https://intl.cloud.tencent.com/document/product/583/37040#.E5.B9.B6.E5.8F.91.E5.AE.9E.E4.BE.8B.E5.A4.8D.E7.94.A8.E4.B8.8E.E5.9B.9E.E6.94.B6">instance repossession</a>.</ul></td>
</tr><tr>
<td>435<br>FunctionNotFound</td>
<td>The function is not found.</td>
<td><ul class="params"><li>Check whether the input parameters match the information of the function to be invoked.</li><li>Check whether the function exists when it is invoked and whether there is any deletion action that causes the function to be invoked after deletion.</li></ul></td>
</tr><tr>
<td>436<br>InvalidParameterValue</td>
<td>The parameter passed in for `invoke` does not conform to the specification.</td>
<td>The parameter does not conform to the specification. Modify it as instructed in <a href="https://intl.cloud.tencent.com/document/product/583/17234">Introduction</a> and try again.</td>
</tr><tr>
<td>437<br>HandlerNotFound</td>
<td>The function package is loaded incorrectly.</td>
<td><ul class="params"><li>Check whether the compressed package is in normal status.</li><li>The function execution entry file is not found. Make sure that the entry file is in the root directory of the decompressed code package.</li><li>Check the entry file and <a href="https://intl.cloud.tencent.com/document/product/583/19805">execution method</a> in the code package.</li></ul></td>
</tr><tr>
<td>438<br>FunctionStatusError</td>
<td>The function is abnormal or the SCF service is suspended.</td>
<td><ul class="params"><li>The function is invoked in an abnormal state. Wait for the function status to become normal and try again.</li>
	<li>The SCF service is suspended because the Tencent Cloud account has overdue payments. Top up and try again.</li></ul></td>
</tr><tr>
<td>439<br>User process exit when running</td>
<td>The user process exits accidentally.</td>
<td><ul class="params"><li>Based on the error message, find out the cause, fix the function code, and try again.</li><li>This status code will trigger <a href="https://intl.cloud.tencent.com/document/product/583/37040#.E5.B9.B6.E5.8F.91.E5.AE.9E.E4.BE.8B.E5.A4.8D.E7.94.A8.E4.B8.8E.E5.9B.9E.E6.94.B6">instance repossession</a>.</td>
</tr><tr>
<td>441<br>UnauthorizedOperation</td>
<td>CAM authentication fails.</td>
<td>Check whether the CAM authentication parameters for the function invoker are passed correctly. For more information, see the authorization description in <a href="https://intl.cloud.tencent.com/document/product/583/18014" >Permission Management Overview</a>.</td>
</tr><tr>
<td>442<br>QualifierNotFound</td>
<td>The specified version is not found.</td>
<td>The function version does not exist. Check the function version and try again.</td>
</tr><tr>
<td>443<br>UserCodeError</td>
<td>A user code execution error occurs.</td>
<td>Based on the error log on the console, check the error stack of the code and see whether the code can be executed properly.</td>
</tr><tr>
<td>444<br>PullImageFailed</td>
<td>Image pull fails.</td>
<td>Check the integrity and validity of the selected image and try again; for example, check whether it can be downloaded locally. If the problem persists, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket.</td>
</tr><tr>
<td>445<br>ContainerInitError</td>
<td>Container start fails.</td>
<td>Container start fails. Check whether your bootstrap file has been uploaded successfully and ensure that the invocation path is correct.<ul class="params"><li>For an image deployment-based function, check whether the `Command` or `Args` parameter passed in the console is in the correct format. For more information, see <a href="https://cloud.tencent.com/document/product/583/56052">Usage</a>.</li><li>For a code deployment-based function, check whether your bootstrap file has been uploaded successfully and ensure that the invocation path is correct.</li></ul></td>
</tr><tr>
<td>446<br>PortBindingFailed</td>
<td>Port listening fails.</td>
<td>The container initialization duration exceeds the <a href="https://intl.cloud.tencent.com/document/product/583/19805">initialization timeout period</a>.<li>Check whether the listening port is<code>9000</code>.</li><li>Check whether all the files in the code package or container image are required files. Appropriate streamlining can improve the initialization speed of the container.</li><li>Check whether there are any exceptions or time-consuming business logic in the initialization code. You can appropriately increase the initialization timeout period and try again.</li></td>
</tr><tr>
<td>447<br>PullImageTimeOut</td>
<td>Image pull times out.</td>
<td>It may be a timeout caused by a large image or network jitters. Minimize the image or increase the <a href="https://intl.cloud.tencent.com/document/product/583/19805">initialization timeout period</a> and try again. If the problem persists, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr><tr>
<td>449<br>InsufficientResources</td>
<td>There are no resources available at the resource specification selected by this function in the specified region.</td>
<td>If the resource type is high-spec CPU or GPU, it can be used with the provisioned concurrency. If the problem persists, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr><td>450<br>InitContainerTimeout</td>
<td>Container start times out.</td>
<td>The container start duration exceeds the <a href="https://intl.cloud.tencent.com/document/product/583/19805">initialization timeout period</a>. Minimize the code or increase the initialization timeout period and try again.</td>
</tr><td>499<br>RequestCanceled</td>
<td>The function execution request is canceled.</td>
<td><ul class="params"><li>For an asynchronously executed function, if the user cancels the function execution request, this message will be returned.</li><li>For an HTTP-triggered function, if the timeout period of an API Gateway trigger is less than the sum of the initialization duration and execution duration of the function, this message will be returned. Check whether there is any abnormally time-consuming business logic in the code or increase the backend timeout period of the API and try again.</li></ul></td>
</tr><tr>
<td>500<br>InternalError</td>
<td>An internal error occurs.</td>
<td>An internal error occurs. Try again later. If the problem persists, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr></tbody>
</table>

## Concepts

#### Execution method<div id="handler"></div>

The execution method specifies the starting file and function while invoking the cloud function as shown below: 
![](https://main.qcloudimg.com/raw/81835da7292ef575fde6d634a99bb1e5.png)

- For Go programming, use the **FileName** format, such as `main`.

- For Python, Node.js, or PHP programming, use the **FileName.FunctionName** format, such as `index.main_handler`.
  - Note that **FileName does not include the file name extension, and FunctionName is the name of the entry function.** Make sure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`, and for Node.js programming, the file name extension is `.js`. For more information, see "Execution Method" in [Basic Concepts](https://intl.cloud.tencent.com/document/product/583/9210).   

- For Java programming, use the **package.class::method** format, such as `example.Hello::mainHandler`.

- For custom runtime, you can ignore the above patterns, and write the execution method in your custom language.
