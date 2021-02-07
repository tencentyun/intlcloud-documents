## January 2021
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
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
<th width=15%>Release Date</th>
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
<th width=15%>Release Date</th>
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
<th width=15%>Release Date</th>
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
<td><a href="https://intl.cloud.tencent.com/zh/document/product/628/38833">Viewing API Statistics/a></td>
</tr></table>

## September 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Experience optimization</td>
<td><li>You can view API documentation in the rich text or Markdown format.</li><li>After you return from the API details page to the API list page, the search parameters and paging parameters are retained, facilitating API management.</li></td>
<td>2020-08-20</td>
<td>-</td>
</tr><tr>
<td>Tags supported</td>
<td>Tags can be added for API Gateway services so that users can manage cloud resources using tags.</td>
<td>2020-08-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/651">Tag</a></td>
</tr><tr>
<td>Experience optimization</td>
<td>A new overview page is available for the API Gateway console, with multiple added features such as quick access, exception alarms, quota limits, and announcements.</td>
<td>2020-08-05</td>
<td>-</td>
</tr></table>

## July 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Experience optimization</td>
<td>The API Gateway console supports quick service deletion and batch service deletion.</td>
<td>2020-07-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11790">Service Deletion</a></td>
</tr></table>

## June 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported alias configuration</td>
<td>When the API backend is interconnected with Serverless Cloud Function (SCF), alias configuration is supported.</td>
<td>2020-06-20</td>
<td>-</td>
</tr></table>

## May 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Identity verification requirements</td>
<td>Identity verification requirements are added. Users who do not pass the identity verification cannot access the API Gateway.</td>
<td>2020-05-31</td>
<td>-</td>
</tr><tr>
<td>Log search upgrade</td>
<td>You can search for service logs using operators, which help you locate problems in massive amounts of log data more efficiently.</td>
<td>2020-05-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/34636">View Log Analysis</a></td>
</tr></table>

## April 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Experience optimization</td>
<td>You can view access monitoring data at the environment granularity.</td>
<td>2020-04-15</td>
<td>-</td>
</tr><tr>
<td>Experience optimization</td>
<td>You can view monthly summary data on the overview page in the API Gateway console.</td>
<td>2020-04-15</td>
<td>-</td>
</tr><tr>
<td>API importing</td>
<td>OpenAPI definitions can be imported into the API Gateway to create APIs, which improves the development experience.</td>
<td>2020-04-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/37875">Importing APIs</a></td>
</tr><tr>
<td>Access to CloudAudit</td>
<td>Access to CloudAudit is officially supported, allowing you to view operation logs independently.</td>
<td>2020-04-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/35597">Viewing Operation Logs</a></td>
</tr></table>

## March 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Cloud API 3.0 supported</td>
<td>Cloud API 3.0 is fully supported, which improves the development experience.</td>
<td>2020-03-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/36595">API Category</a></td>
</tr><tr>
<td>Experience optimization</td>
<td>The time for which you can continue to use the API Gateway service after your account falls into arrears is extended from 2 hours to 24 hours.</td>
<td>2020-03-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11934">Notes on Arrears</a></td>
</tr></table>

## February 2020
<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Service log exporting</td>
<td>The real-time service log feature supports log exporting, facilitating multi-dimensional data analysis and problem location for users.</td>
<td>2020-02-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/37876">Exporting Service Logs</a></td>
</tr><tr>
<td>Official billing</td>
<td>API Gateway is officially commercialized. Billable items include API call fees and traffic fees.</td>
<td>2020-02-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/11771">Pay-As-You-Go</a></td>
</tr></table>
