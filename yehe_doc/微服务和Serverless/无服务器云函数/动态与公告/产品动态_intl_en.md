## November 2021

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for provisioned concurrency</td>
<td>SCF supports configuring the provisioned concurrency to prepare computing resources in advance and reduce the duration for cold start and initialization of runtime environment and business code.</td><td>2021-11-01</td><td>
<a href="https://intl.cloud.tencent.com/document/product/583/37704">Provisioned Concurrency</a>
</td>
</tr>
</tbody></table>

## July 2021

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for deployment of multiple web frameworks</td>
<td>SCF allows you to deploy a local project to the cloud through an HTTP-triggered function.</td>
<td>2021-07-29</td>
<td>
<a href="https://intl.cloud.tencent.com/zh/document/product/583">Web Framework Deployment</a>
</td>
</tr>
</tbody></table>


## July 2021

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for container image delivery of SCF</td>
<td>SCF supports container image delivery, richer repository types, non-intrusive log collection and aggregation, image pull based on image digest, and custom image, so that you don't need to modify the code or recompile binary dependencies, which accelerates the serverless transformation of your applications.</td>
<td>2021-06-08</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/583/41076">Feature Description</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/583/41077">Usage</a></li>
</td>
</tr>
</tr>
</thead>
<tbody>
<tr>
<td>New HTTP-triggered functions</td>
<td>SCF supports creating HTTP-triggered functions that can accept and process native HTTP requests.
</td>
<td>2021-06-08</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/583/40688">HTTP-Triggered Function Overview</a>
</td>
</tr>
</tbody></table>

## January 2021

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added retry capability for async SCF invocation</td>
<td>
<li>
Added support for modifying the configurations of retry and maximum retention for async invocations. You can control the retry capabilities of function resources through relevant configurations.</li>
<li>Updated the function overrun retry policy, eliminating your need to concern over data retry failures caused by overrun. Functions will make special retries for overrun errors by default.</li>
</td>
<td>2021-01-18</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/583/39704">Dead Letter Queue</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/583/39851">Error Types and Retry Policies</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/583/39848">Concurrency Overrun</a></li></td>
</tr>
</tbody></table>

## December 2020

<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Upgraded the function creation process</td>
<td><li>Simplified the function creation process for quicker creation.</li>
<li>Added support for configurations for template-based function creation.</li>
<li>Added support for trigger configurations for function creation.</li>
<li>Interconnected with Serverless Framework for creating applications in the SCF console.</li>
<li>Interconnected with CODING for deploying functions and applications through CI.</li></td>
<td>2020-12-30</td>
<td>-</td>
</tr>
<tr>
<td>Released the async function execution feature</td>
<td>SCF provides the async function execution mode to extend the execution timeout period and solve the problems with existing execution mechanisms.</td>
<td>2020-12-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39466">Async Execution</a>
</td>
</tr>
<tr>
<td>Released SCF Serverless Web IDE</td>
<td>SCF and CODING jointly released Serverless Web IDE to provide a development experience closer to local IDE, which supports:
<li>Complete function development, deployment, and testing capabilities.</li>
<li>Terminal capabilities. Common development tools such as pip and npm and programming language development environments already supported by SCF are pre-configured in it.</li>
<li>The basic capabilities of a complete IDE, such as smart prompt and code autocomplete.</li>
<li>User-defined IDE configuration, which ensures a consistent IDE user experience for the development of different functions.</li></td>
<td>2020-12-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39962">Serverless Web IDE</a>
</td>
</tr>
<tr>
<td>Supported MPS triggers</td>
<td>The combination of SCF and MPS enables you to quickly process and manipulate callback events generated by MPS.</td>
<td>2020-12-11</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/583/39339">MPS Function Processing Overview</a>
</td>
</tr>
<tr>
<td>Added support for data sync between SCF API Gateway trigger and API Gateway</td>
<td>Creating, deleting, and updating serverless APIs on the API Gateway side are completely synced with creating, deleting, and updating API Gateway triggers on the SCF side. Changes on one side will be automatically synced to the other side.</td>
<td>2020-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12513">Overview</a>
</td>
</tr>
</tbody></table>





## November 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the online debugging feature</td>
<td>With the online debugging feature of SCF, you can complete checkpoint debugging, use the console, and view the runtime memory and CPU status, so that you can quickly locate problems in the console.</td>
<td>2020-11-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39008">Debugging Function</a>
</td>
</tr>
<tr>
<td>Added support for CLS triggers</td>
<td>You can use SCF to process the logs collected in the CLS service. By passing the collected logs as a parameter, the function can be invoked, where the function code can process and analyze the data or dump it to other Tencent Cloud services.</td>
<td>2020-11-17</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/583/38845">CLS Trigger</a></li>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/583/38847">CLS Function Processing Overview</a></li>
</td>
</tr>
<tr>
<td>Added support for CKafka message dump to ES</td>
<td>SCF is connected with CKafka to allow you to dump messages to Elasticsearch Service (ES) for consumption and management, making it easier to store and search massive amounts of data and analyze logs in real time.</td>
<td>2020-11-17</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/583/37896">Message Dump to ES</a>
</td>
</tr>
</tbody></table>




## August 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the CKafka-to-CKafka dump feature based on SCF</td>
<td>You can use SCF to dump messages from one CKafka topic cluster to another.</td>
<td>2020-08-06</td>
<td>Message Dump to CKafka</a>
</td>
</tr>
<tr>
<td>Released the Custom Runtime feature</td>
<td>SCF provides Custom Runtime to customize the runtime environment. By enabling custom implementation for the function runtime, you can use any version of any programming language to write functions as needed.</td>
<td>2020-08-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/38129">Custom Runtime</a>
</td>
</tr>
</tbody></table>




## July 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Started the beta test of the provisioned concurrency feature</td>
<td>The provisioned concurrency feature can start concurrent instances in advance according to the configuration.</td>
<td>2020-07-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/37704 ">Provisioned Concurrency</a>
</td>
</tr>
<tr>
<td>Added support for CFS file systems</td>
<td>SCF supports mounting CFS file systems to have a larger disk space. It allows different functions to write into the same file system.</td>
<td>2020-07-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/37497">Mounting CFS File System</a>
</td>
</tr>
<tr>
<td>Released the SCF-based CDN cache purge feature</td>
<td>You can quickly configure an SCF-based CDN purge scheme in the COS console.</td>
<td>2020-07-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37273">CDN Cache Purge</a>
</td>
</tr>
</tbody></table>



## June 2020
<table>
<thead>
<tr>

<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the ICP filing feature</td>
<td>If your website is hosted in Tencent Cloud's Serverless service in the Chinese mainland, and the organizer and domain name of the website have never obtained an ICP filing, then you need to perform the initial ICP filing operation in the Tencent Cloud ICP filing system first before activating the Serverless service and using SCF for HTTP access to the custom domain name.</td>
<td>2020-06-12</td>
<td>ICP Filing</a>
</td>
</tr>

<tr>
<td>Released the SCF VS Code plugin</td>
<td>The SCF VS Code plugin was upgraded to v2.0:
The specification used by the plugin was adjusted to the Tencent-SCF Component specification in Serverless Framework.
The original TCSAM-compatible specification can be converted to the Serverless Framework Tencent-SCF Component specification.
Node.js 10.15 and Node.js 12.16 runtime environments were added.
Node.js 10 and above runtime environments were added for cloud debugging.</td>
<td>2020-06-12</td>
<td>SCF VS Code Plugin Usage</a>
</td>
</tr>

<tr>
<td>Added the Node.js 12.16 runtime environment</td>
<td>The Node.js 12.16 runtime environment was added for SCF. You can choose to use Node.js 12.16 as the runtime environment when creating a function. The upgrade of the Node.js version brings new features and performance improvements and, mostly importantly, speeds up launches.</td>
<td>2020-06-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/11060">Notes on Node.js</a>
</td>
</tr>
</tbody></table>



## May 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for providing a fixed outbound IP on the public network</td>
<td><ul><li> When the public network is enabled for a function, a fixed outbound IP on the public network can be enabled to get a randomly assigned EIP. The traffic generated by the function accessing the public network will be forwarded based on the EIP.</li> <li>When both public network access and private network access are enabled for the function, the traffic generated by accessing the public network will be forwarded based on the EIP, while that generated by accessing the private network will be forwarded based on the VPC.</li> </ul></td>
<td>2020-05-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/38106">Fixed Public Outbound IP</a>
</td>
</tr>
<tr>
<td>Added support for installing dependencies online for the Node.js runtime</td>
<td>If "Online install dependency" is enabled in the function configuration, each time the code is uploaded, the SCF backend will check the `package.json` file in the root directory of the code package and try using npm to install the dependent package based on the dependencies in `package.json`. Currently, you can install dependencies online for the Node.js runtime, and each time the code is updated, the SCF backend will automatically install dependencies. </td>
<td>2020-05-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/38105">Online Dependency Installation</a>
</td>
</tr>
</tbody></table>




## April 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for enabling both the public network and VPC</td>
<td>SCF now supports enabling both the public network and VPC, and the code can access resources in the VPC and public network, lowering the configuration complexity. Both or either of the VPC and public network can be enabled.</td>
<td>2020-04-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/38377">Network Configuration Management</a>
</td>
</tr>
<tr>
<td>Released the grayscale release feature</td>
<td>SCF allows you to configure aliases, versions, and traffic routing to switch traffic between multiple versions.<ul><li>Two versions can be configured for an alias, and a rule can be configured to switch traffic between the two versions.</li> <li>Traffic can be routed based on weight or request attribute.</li> <li>A trigger can be configured for an alias.</li> <li>You can view logs and monitoring data by alias or version.</li></ul></td>
<td>2020-04-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/35952">Traffic Routing Configuration</a>
</td>
</tr>
<tr>
<td>Released the layer feature</td>
<td>SCF allows you to use layers to manage dependent libraries and common code files.</td>
<td>2020-04-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/37039">Layer Management</a>
</td>
</tr>
</tbody>
</table>




## March 2020
<table>
<thead>
<tr>
<th width="20%">Update</th>
<th width="40%">Description</th>
<th width="20%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the SCF-based COS file decompression feature</td>
<td>The file decompression feature is a data processing solution provided by COS based on SCF. After it is enabled, when a compressed file is uploaded to COS, the function pre-configured by COS will be automatically triggered to decompress the file to the specified bucket and directory.</td>
<td>2020-03-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/35663">File Decompression</a>
</td>
</tr>
</tbody></table>


