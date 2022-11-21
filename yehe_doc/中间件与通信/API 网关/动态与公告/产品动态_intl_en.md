## June 2022
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The custom plugin supported the proxy backend</td>
<td>API Gateway's custom (verification, response body, and request body) plugins can be bound to a service deployed on the public network or in a VPC, allowing for greater flexibility.</td>
<td>2022-06-20</td>
<td>-</td>
</tr><tr>
<td>Supported the anti-replay plugin</td>
<td>The anti-replay plugin is provided by API Gateway dedicated instances to protect APIs from replay attacks.</td>
<td>2022-06-20</td>
<td>-</td>
</tr><tr>
<td>Marketplace Dashboard was available free of charge for a limited period of time</td>
<td>Tencent Cloud API Gateway releases the Marketplace Dashboard feature, which is available free of charge for a limited period of time.</td>
<td>2022-06-20</td>
<td>-</td>
</tr>
<tr>
<td>Supported multiple backend types for API importing</td>
<td>All the backend types are supported for the API importing feature.</td>
<td>2022-06-20</td>
<td>-</td>
</tr>
<tr>
<td>Supported TLS version control</td>
<td>API Gateway dedicated instances now support TLS versions.</td>
<td>2022-06-20</td>
<td>-</td>
</tr>
<tr>
<td>Billing of the public network outbound traffic from API Gateway to backend services</td>
<td>Starting from 23:59:59 on August 15, 2022, Tencent Cloud API Gateway instances (shared, dedicated, and exclusive instances) will be billed by actual traffic if their access to backend services generates public network outbound traffic.</td>
<td>2022-06-20</td>
<td>-</td>
</tr>
</table>

## October 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported the conditional routing plugin</td>
<td>The conditional routing plugin provides the capability to forward different client requests to different backend addresses according to the requested parameter values and system parameter values. It can be widely used in scenarios such as canary release, blue-green deployment and tenant routing.</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/44308">Conditional Routing Plugin</a></td>
</tr><tr>
<td>Mainstream resources supported tagging</td>
<td>Mainstream API Gateway resources such as instances, plugins, and applications support tagging and authorization based on tags, reducing your cost of managing API Gateway resources.</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/651">Tag</a></td>
</tr><tr>
<td>Released Cloud Native Gateway</td>
<td>Cloud Native Gateway is an API gateway hosting product incubated by Tencent Cloud that is 100% compatible with the open-source Kong gateway. It is fully compatible with open-source resources and eliminates deployment or Ops. It features high performance and high reliability and supports Tencent Cloud plugins, greatly reducing your costs of setting up gateways.</td>
<td>2021-10-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/47414">Creating Cloud Native Gateway</a></td>
</tr></table>



## September 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported the custom request body plugin</td>
<td>The custom request body plugin is based on Serverless Cloud Function (SCF) and applies during request process. The API Gateway will forward the request content to the specified SCF after receiving it from the client. SCF will send the modified content of the request body to the API Gateway after modifying it. Then, the API Gateway will forward the modified request body to the backend.</td>
<td>2021-09-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/44381">Custom Request Body</a></td>
</tr><tr>
<td>Supported the custom verification plugin</td>
<td>The custom verification plugin applies during the request process. API Gateway will forward the request to the verification function after receiving it from the client. Then, the request will be forwarded to the service backend only if it passes the verification by the function; otherwise, the request will be denied.</td>
<td>2021-09-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/44380">Custom Verification</a></td>
</tr></table>



## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported upstreams</td>
<td>API Gateway supports connection of backends with upstreams to forward requests to multiple nodes on backends directly without through private CLBs.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/42044">Upstreams</a></td>
</tr></table>



## July 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported custom CORS plugin</td>
<td>If the default CORS configuration of API Gateway cannot meet your needs, you can configure custom complex CORS rules through the CORS plugin and bind it to APIs.</td>
<td>2021-07-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/41450">CORS</a></td>
</tr></table>



## June 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Disaster recovery across AZs was supported by dedicated instances</td>
<td>You can choose up to two AZs at a time for deployment when purchasing a dedicated instance to improve the reliability.</td>
<td>2021-06-27</td>
<td>-</td>
</tr><tr>
<td>4XX and 5XX error codes monitoring was supported</td>
<td>4XX and 5XX error codes monitoring metrics are integrated to provide corresponding warnings.</td>
<td>2021-06-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/34888">Monitoring Metrics</a></td>
</tr><tr>
<td>Dedicated instances were officially launched</td>
<td>API Gateway officially launches dedicated instances. The underlying resources of a dedicated instance are exclusive to the user. Compared with a shared instance, a dedicated instance can provide higher performance and SLA guarantee and thus is more suitable for use in production environments by large companies.</td>
<td>2021-06-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/40305">Instance Specification</a></td>
</tr></table>



## May 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported connection of backends with EventBridge</td>
<td>API Gateway supports connection of backends with EventBridge, and the APIs hosted in the API Gateway are used as the event bus entry.</td>
<td>2021-05-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1108/42279">APIGW connector</a></td>
</tr><tr>
<td>Optimization of importing/exporting APIs</td>
<td>Importing/exporting APIs supports importing/exporting of APIs in the SCF backend.</td>
<td>2021-05-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/37874">Defining APIs</a></td>
</tr><tr>
<td>Basic traffic throttling plugin was supported</td>
<td>The basic traffic throttling plugin is a powerful traffic throttling component provided by API Gateway. It can throttle traffic in three dimensions of API, application, and client IP by second, minute, hour, or day.</td>
<td>2021-05-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/40307">Basic Traffic Throttling</a></td>
</tr></table>



## April 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Optimized service log search</td>
<td>Real-Time service logs can be searched for by environment and path.</td>
<td>2021-04-14</td>
<td>-</td>
</tr><tr>
<td>Released API Doc Generator</td>
<td>You can use API Doc Generator to generate exquisite API documents for APIs hosted in API Gateway and provide them to third-party callers of your APIs.</td>
<td>2021-04-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/40212">API Doc Generator</a></td>
</tr><tr>
<td>Released the plugin feature</td>
<td>Plugins are advanced feature configurations provided by API Gateway. You can create configuration items such as IP access control through plugins and then bind the plugins to APIs for them to take effect.</td>
<td>2021-04-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/40214">Plugins</a></td>
</tr></table>



## January 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Base64 Encoding</td>
<td>When the connected backend is SCF, enabling Base64 encoding is available. API Gateway will Base64-encode the requested content and forward it to SCF for binary data upload.</td>
<td>2021-01-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/39489">Base64 Encoding</a></td>
</tr><tr>
<td>Optimized monitoring</td>
<td>The service statistics feature is added. You can view the statistics of all services under your account within a day to quickly locate problems. </td>
<td>2021-01-21</td>
<td>-</td>
</tr></table>


## December 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the mandatory HTTPS feature for custom domain name</td>
<td>On the custom domain name configuration page, if the protocol is HTTPS&HTTPS or HTTPS, the mandatory HTTPS feature can be enabled. After it is enabled, API Gateway will redirect requests using the custom domain name over the HTTP protocol to the HTTPS protocol.</td>
<td>2020-12-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11791">Configuring a Custom Domain Name</a></td>
</tr><tr>
<td>Supported JSON data during WebSocket protocol connection to SCF</td>
<td>When the WebSocket protocol is connected to SCF, data in JSON type is supported.</td>
<td>2020-12-18</td>
<td>-</td>
</tr><tr>
<td>Synced trigger data</td>
<td>The issue where the data was out of sync between the SCF APIs connected to API Gateway and the API Gateway triggers of SCF is fixed, so that no matter on which side the data is modified, corresponding changes will be made on the other side.</td>
<td>2020-12-02</td>
<td>-</td>
</tr></table>


## November 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported response compression</td>
<td>Response compression based on the gzip algorithm is supported, which can effectively reduce the transferred data amount, response time, and server network bandwidth usage and improve the client performance.</td>
<td>2020-11-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/38851">Compressing Responses</a></td>
</tr></table>


## October 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Adjusted billing</td>
<td><li>The billing mode of resource pack (prepaid) is added. Resource packs can be obtained through free tier and marketing campaigns.</li><li>Free tier is implemented through resource packs, which will be automatically rewarded when a new user activates the API Gateway service.</li></td>
<td>2020-10-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/38407">Resource Pack (Prepaid)</a></td>
</tr><tr>
<td>Optimized monitoring</td>
<td>The API statistics feature is added. You can view the statistics of all APIs under the service within a day to quickly locate problems.</td>
<td>2020-10-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/38833">Viewing API Statistics</a></td>
</tr></table>


## September 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Signature tool added</td>
<td>The API Gateway signature tool is a web tool provided by Tencent Cloud API Gateway to generate request signatures for key pair authentication APIs.</td>
<td>2020-09-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/38376">Signature Tool</a></td>
</tr></table>


## August 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Optimized experience</td>
<td><li>You can view API documents in the rich text or Markdown format.</li><li>After you return from the API details page to the API list page, the search parameters and paging parameters are retained, facilitating API management.</li></td>
<td>2020-08-20</td>
<td>-</td>
</tr><tr>
<td>Tags supported</td>
<td>Tags can be added for API Gateway services so that users can manage cloud resources using tags.</td>
<td>2020-08-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/651">Tag</a></td>
</tr><tr>
<td>Optimized experience</td>
<td>A new overview page is available for the API Gateway console, with multiple added features such as quick access, exception alarms, quota limits, and announcements.</td>
<td>2020-08-05</td>
<td>-</td>
</tr></table>


## July 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Optimized experience</td>
<td>API Gateway console supports quick deletion and batch deletion of services.</td>
<td>2020-07-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11790">Deleting Services</a></td>
</tr></table>


## June 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported alias configuration</td>
<td>Alias configuration is supported when API backends are connected with SCFs.</td>
<td>2020-06-20</td>
<td>-</td>
</tr><tr>
</tr></table>


## May 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Identity verification was required</td>
<td>Identity verification is added. Users who have not passed identity verification cannot access the API Gateway.</td>
<td>2020-05-31</td>
<td>-</td>
</tr><tr>
<td>Log search upgraded</td>
<td>Operator search is supported for service logs. Therefore, issues can be located more effectively.</td>
<td>2020-05-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/34636">View Log Analysis</a></td>
</tr></table>


## April 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Optimized experience</td>
<td>Viewing monitoring graphs is supported at the environment granularity.</td>
<td>2020-04-15</td>
<td>-</td>
</tr><tr>
<td>Optimized experience</td>
<td>Monthly aggregate data can be viewed on the overview page in the console.</td>
<td>2020-04-15</td>
<td>-</td>
</tr><tr>
<td>Importing APIs was supported</td>
<td>It supports importing OpenAPI definition to API Gateway to create APIs.</td>
<td>2020-04-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/37875">Importing APIs</a></td>
</tr><tr>
<td>CloudAudit was integrated</td>
<td>CloudAudit is integrated. Users can view operation logs independently.</td>
<td>2020-04-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/35597">Viewing Operation Logs</a></td>
</tr></table>


## March 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Cloud API 3.0 was supported</td>
<td>Cloud API 3.0 is fully supported.</td>
<td>2020-03-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/36595">API Doc Generator</a></td>
</tr><tr>
<td>Optimized experience</td>
<td>You can continue to use the API Gateway service within 24 hours (inclusive) after your account has overdue payment.</td>
<td>2020-03-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11934">Notes on Overdue Payment</a></td>
</tr></table>


## February 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Service logs can be exported</td>
<td>With the real-time service log feature, you can export logs for data analysis and problem location.</td>
<td>2020-02-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/37876">Exporting Service Logs</a></td>
</tr><tr>
<td>Started charging</td>
<td>We started charging on API Gateway. There are two billing items, including API calls and traffic.</td>
<td>2020-02-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11771">Billing Overview</a></td>
</tr></table>
