## December 2022

<table>
<thead>
<tr>
<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Optimized the log index failure policy</td>
<td>An index may fail to be created due to the abnormal raw log format or index configuration mismatch. CLS allows for storing raw logs separately for exception handling. This ensures that logs won't be lost.</td>
<td>2022-12-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/39594">Configuring Index</a></td>
<tr>
<td>Added encoding/decoding and encryption functions to alarm notification variables</td>
<td>Base64/Base64URL/URL encoding and decoding, MD5/SHA1/SHA256/SHA512 encryption, and HMAC_MD5/HMAC_SHA1/HMAC_SHA256/HMAC_SHA512 encryption are supported for alarm notification variables to generate signature strings required for custom callback API authentication.</td>
<td>2022-12-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/41984">Alarm Notification Variable</a></td>
</tr>
<tr>
<td>Added data preview for shipping to CKafka/COS</td>
<td>The log data format to be shipped can be intuitively previewed in the console, increasing the efficiency.</td>
<td>2022-12-25</td>
<td>-</td>
</tr>
<tr>
</tr>
<td>Supported custom variables for the dashboard</td>
<td>Variable values can be set and applied to search statements, titles, and text in charts to batch modify statements.</td>
<td>2022-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/43561">过滤与变量</a></td>
</tr>
</tbody></table>

## November 2022

<table>
<thead>
<tr>
<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supported field configuration for dashboard charts</td>
<td>You can configure a personalized style for a single field in a chart, so as to make the dashboard more varied in style.</td>
<td>2022-11-25</td>
<td>-</td>
<tr>
<td>Supported multiple log topics for an alarm policy</td>
<td>Up to 20 log topics can be set for an alarm policy. It can be determined whether the trigger conditions are met separately for each log topic. Currently, selected log topics must be in the same region.</td>
<td>2022-11-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/39574">Configuring Alarm Policy</a></td>
</tr>
<tr>
<td>Upgraded the dashboard filter</td>
<td>Static option input and alias configuration are supported in the dashboard filter drop-down list. In addition, filter by search statement is supported, including filter by range, NOT, full text, or fuzzy match, meeting different requirements.</td>
<td>2022-11-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/43561">过滤与变量</a></td>
</tr>
<tr>
</tr>
<td>Added a function for data processing</td>
<td>The `ext_grok` function is added for data processing, which extracts the matched result value based on the Grok syntax, making it easier to extract a key-value pair with a regular expression when a processing function is used.</td>
<td>2022-11-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/45595">键值提取函数</a></td>
</tr>
</tbody></table>





## October 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Supported custom redirect links in the dashboard</td><td>Another page can be redirected to by clicking a field in a chart. The URL to be redirected to can be a variable to cater to personalized needs. Currently, only tables are supported, with more chart types to come.</td><td>2022-10-24</td><td><a href="https://cloud.tencent.com/document/product/614/82034">Custom Redirect</a></td></tr>
		<tr><td>Supported monitoring of log shipping tasks to CKafka</td><td>The traffic, number of lines, status, and latency of shipping tasks to CKafka can be monitored, so that users can stay on top of task details and better manage shipping tasks.</td><td>2022-10-12</td><td>-</td></tr>
		<tr><td>Supported log transition for STANDARD log topics.</td><td>Log transition can be enabled for STANDARD log topics, so that legacy data can be transitioned to STANDARD_IA for long-term storage. The transitioned data will be billed by STANDARD_IA storage, which meets the requirements for real-time alarm analysis and low-cost storage.</td><td>2022-10-11</td><td><a href="https://cloud.tencent.com/document/product/614/82172">Log Transition</a></td></tr>
				<tr><td>Supported the interactive mode for search and analysis</td><td>Log search and analysis can be performed with a click to automatically generate statements including SQL, making it easier to learn statements.</td><td>2022-10-10<td>-</td></tr>
					<tr><td>Supported import and export for the dashboard</td><td>Dashboard files can be imported and exported to meet the requirements for cross-account dashboard migration and sharing.</td><td>2022-10-09</td><td>-</td></tr>
	</tbody>
</table>



## September 2022


<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Added log charts for dashboards</td><td>You can add and browse raw logs on the dashboard page. The analysis result and associated log content are displayed on the dashboard with no redirects needed, making operations easier.</td><td>2022-09-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50844">Log</a></td></tr>
		<tr><td>Supported LogListener for syslog collection</td><td>You can use LogListener to collect Linux syslog and quickly configure collection rules in the CLS console.</td><td>2022-09-15</td><td><a href="https://cloud.tencent.com/document/product/614/81454">Syslog Collection</a></td></tr>
		<tr><td>Supported trigger by group in the alarm policy</td><td>If multiple results of the execution result meet the alarm trigger condition, the results will be grouped based on the group field, and an alarm will be triggered for each group.</td><td>2022-09-06</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39574">Configuring Alarm Policy</a></td></tr>
	</tbody>
</table>




## August 2022
<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Supported dashboard subscription via email</td><td>CLS allows users to subscribe to a dashboard and export it as an image. Daily, weekly, and monthly reports can be emailed to specified recipients regularly. This is suitable for scenarios where dashboards need to be published regularly and reduces costs.</td><td>2022-08-29</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50277">Subscribing to Dashboard</a></td></tr>
		<tr><td>Supported data compression for consumption over Kafka</td><td>Consumption over Kafka supports data compression, which greatly reduces the read traffic volume and costs.</td><td>2022-08-25</td><td><a href="https://intl.cloud.tencent.com/document/product/614/42752">Consumption over Kafka</a></td></tr>
		<tr><td>Supported monitoring of shipping tasks to COS</td><td>The traffic, number of lines, status, and latency of shipping tasks to COS can be monitored, so that users can stay on top of task details and better manage shipping tasks.</td><td>2022-08-23</td><td><a href="https://intl.cloud.tencent.com/document/product/614/30440">Shipping Task Management</a></td></tr>
		<tr><td>Added Parquet format for shipping to COS</td><td>CLS supports shipping log data in Parquet format to COS, which is suitable for big data computing and analysis scenarios where Hive is at downstream.</td><td>2022-08-23</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50279">Parquet Shipping</a></td></tr>
		<tr><td>Added random sampling mode for statistical log analysis</td><td>CLS supports random sampling and analysis of massive amounts of data in raw logs. Compared with full analysis, it can achieve an accuracy of over 95% and solve the problems of slowness and timeout in full analysis, meeting the requirements for statistical analysis in various business scenarios.</td><td>2022-08-22</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50243">Sampling Analysis</a></td></tr>
	</tbody>
</table>

## July 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Added funnel chart to dashboards</td><td>Users can collect the statistics of business processes with single flow and path and then intuitively compare conversion rates in different stages.</td><td>2022-07-20</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50242">Funnel Chart</a></td></tr>
		<tr><td>Released the scheduled SQL analysis feature</td><td>Search statements are executed based on custom cycles and times, and results are saved in new log topics. This greatly reduces the query failure rate and costs.</td><td>2022-07-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50239">Overview</a></td></tr>
		<tr><td>Supported reporting data from mobile devices through the SDK</td><td>Log information such as network detection can be reported from mobile devices through the SDK for Android/iOS.</td><td>2022-07-01</td><td><a href="https://intl.cloud.tencent.com/document/product/614/45006">Uploading Log via SDK</a></td></tr>
	</tbody>
</table>

## June 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Supported custom chart time in dashboards</td><td>The chart time can be independent and doesn't change as the global time changes. In the dashboard, different charts can use different times to support more diversified comparisons.</td><td>2022-06-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50275">Custom Chart Time</a></td></tr>
		<tr><td>Added DSL functions for data processing</td><td>DSL functions are added for data processing, covering IP parsing, codec, and more scenarios.</td><td>2022-06-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/45594">Function Overview</a></td></tr>
		<tr><td>Released preset dashboards</td><td>CLS supports accessing the standard logs of multiple Tencent Cloud products and provides out-of-the-box log analysis dashboards for visual analysis.</td><td>2022-06-27</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50276">Preset Dashboard</a></td></tr>
		<tr><td>Upgraded notification content variables </td><td>More notification content variables are supported, which can be extracted, escaped, and formatted.</td><td>2022-06-16</td><td><a href="https://intl.cloud.tencent.com/document/product/614/41984">Notification Content Variable</a></td></tr>
		<tr><td>Added the index recreation feature</td><td>After index configurations are modified, indexes can be recreated for historical log data, so that it can be searched for and analyzed based on new configurations.</td><td>2022-06-10</td><td><a href="https://intl.cloud.tencent.com/document/product/614/50278">Reindexing</a></td></tr>
	</tbody>
</table>

## May 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Added demos for four Tencent Cloud products</td><td>Demos are added for CDN, FlowLog, TKE, and COS, helping users try out CLS features.</td><td>2022-05-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43572">CLB Analysis Scenario Experience Demo</a></td></tr>
		<tr><td>Supported log upload over Kafka</td><td>Kafka configurations are added in the console, where Kafka output configurations are automatically generated based on the uploaded Kafka producer and account information. Users can copy existing configurations for quick upload.</td><td>2022-05-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43574">Uploading Log over Kafka</a></td></tr>
	</tbody>
</table>

## April 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Supported automatic unit conversion in dashboards</td><td>Chart units can be automatically converted. When a value meets the conversion factor, it will be automatically converted to the next higher unit, making data more readable.</td><td>2022-04-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/47788">Unit Configuration</a></td></tr>
		<tr><td>Supported trend comparison of sequence diagrams</td><td>Sequence diagrams support adding trend comparison curves of past cycles, enhancing the capabilities of comparative chart analysis.</td><td>2022-04-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/47779">Sequence Diagram</a></td></tr>
		<tr><td>Consumption over Kafka in all regions</td><td>You can consume data to downstream big data components or data warehouses over the Kafka protocol, such as self-built Kafka clusters, ClickHouse, Hive, and Flink, as well as Tencent Cloud EMR and Oceanus.</td><td>2022-04-20</td><td><a href="https://intl.cloud.tencent.com/document/product/614/42752">Consumption over Kafka</a></td></tr>
		<tr><td>Use of SQL to collect and analyze historical data when the index configuration is modified</td><td>When the index configuration is modified, users can use SQL to collect and analyze historical data for existing fields in the original configuration (but not for new fields).</td><td>2022-04-18</td><td>-</td></tr>
		<tr><td>Metadata collection range selection for container collection</td><td>You can select one or more container metadata fields collected by default and configure whether to enable index.</td><td>2022-04-13</td><td>-</td></tr>
		<tr><td>Adding metadata/preset fields to full-text index</td><td>You can add metadata/preset fields to full-text index during index configuration for full-text search of such fields.</td><td>2022-04-12</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39594">Configuring Indexes</a></td></tr>
	</tbody>
</table>


## March 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Word cloud in dashboard</td><td>The word cloud feature is launched to visualize text data and highlight frequent words.</td><td>2022-03-15</td><td>-</td></tr>
	</tbody>
</table>


## February 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>CLS joining Grafana's official plugin market</td><td><ul  style="margin: 0;"><li>The Grafana plugin for CLS can be installed with a few clicks.</li><li>The plugin comes with multiple cloud product templates and can be used out-of-the-box.</li><li>The plugin provides comprehensive analysis capabilities.</li></ul></td><td>2022-02-25</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39592">CLS Connection to Grafana</a></td></tr>
		<tr><td>Visual map reconstruction</td><td><ul  style="margin: 0;"><li>Added support for filtering map display areas by scrolling the legend scope.</li><li>Fixed the occasional overlap problem of legends.</li><li>Optimized the color display of maps to separate regions without data.</li></ul></td><td>2022-02-20</td><td>-</td></tr>
	</tbody>
</table>

## January 2022

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Support for permanent retention of log topics</td><td>You can customize the log topic retention period to a value ranging from 1 to 3600 days or enable permanent retention.</td><td>2022-01-25</td><td><a href="https://intl.cloud.tencent.com/document/product/614/37887">Specifications</a></td></tr>
		<tr><td>Launch of the index configuration import feature</td><td>You can import the index configuration rules of existing log topics with a few clicks to improve efficiency.</td><td>2022-01-18</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39594">Configuring Indexes</a></td></tr>
	</tbody>
</table>

## December 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Support for log upload via Kafka</td><td><ul  style="margin: 0;"><li>Supported Kafka protocol versions: 0.11.X-2.8</li><li>Supported data compression modes: Gzip, Snappy, lz4, zstd</li></ul></td><td>2021-12-27</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43574">Uploading Logs via Kafka</a></td></tr>
		<tr><td>Updated TKE log collection</td><td><ul  style="margin: 0;"><li>Log collection configuration supports `label !=` operations (exclude labels).</li><li>Log collection configuration supports selecting multiple namespaces or excluding namespaces.</li><li>Supports incremental log collection.</li><li>Supports manual upgrade of LogListener.</li></ul></td><td>2021-12-21</td><td><a href="https://intl.cloud.tencent.com/document/product/457/46845">CLS Add-on Version Description</a></td></tr>
		<tr><td>Supported viewing log topic usage in the Cloud Monitor dashboard</td><td>Usage metrics such as the log storage size and write traffic and corresponding alarms are delivered to the Cloud Monitor dashboard so that users can view the usage of log topics in a centralized manner.</td><td>2021-12-17</td><td><a href="https://www.tencentcloud.com/document/product/248/13117">	Cloud Monitor</a></td></tr>
		<tr><td>Optimized dashboard visual data configuration</td><td>Dashboard visual data configuration now supports the new features of displaying hidden fields and aggregating metrics by groups.</td><td>	2021-12-15</td><td>-</td></tr>
		<tr><td>Support for importing COS data to CLS</td><td>	 You can import COS data to CLS for various purposes, such as search, analysis, and data processing and cleansing.</td><td>2021-12-10</td><td><a href="https://intl.cloud.tencent.com/document/product/614/45468">Importing COS Data</a></td></tr>
	</tbody>
</table>


## November 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>CLS feature experience demo available</td><td>For product trial and test scenarios, the free demo provides quick data access and feature templates to help you access content close to real-life scenarios easily and quickly.</td><td>2021-11-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43572">CLB Analysis Scenario Experience Demo</a></td></tr>
		<tr><td>STANDARD_IA in beta testing in some regions</td><td>STANDARD_IA is a low-cost log storage solution to search and store massive infrequently accessed logs, meeting users' requirements for backtracking and archiving historical logs. The solution applies to scenarios where users do not have log statistical analysis requirements and logs need to be stored for a long time. (In the beta test period, the solution is available only in Beijing, Guangzhou, Shanghai, and Hong Kong, China.)</td><td>2021-11-30</td><td><a href="https://intl.cloud.tencent.com/document/product/614/42004">Offline Storage</a></td></tr>
		<tr><td>Connecting self-built Kubernetes clusters to CLS</td><td>You can use the console to configure log collection rules to quickly connect self-built Kubernetes clusters to CLS, reducing learning and use costs.</td><td>2021-11-26</td><td><a href="https://www.tencentcloud.com/document/product/614/42745">Connecting Self-Built Kubernetes Cluster to CLS</a></td></tr>
		<tr><td>Data processing feature released</td><td>Data processing provides the capability to structure, filter, mask, distribute, and enrich log data, which provides the basis for structured data search, analysis, and dashboard display of log data.</td><td>2021-11-22</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43568">Data Processing</a></td></tr>
		<tr><td>Support for logs uploaded via Kafka</td><td>CLS is compatible with Kafka to be compatible with open-source ecosystems. You only need to modify the write source of your existing system to achieve quick access and support various open-source collection components such as Logstash, Fluentd, and Filebeat.</td><td>2021-11-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43574">Uploading Logs via Kafka</a></td></tr>
		<tr><td>Support for downloading up to 50 million logs at a time</td><td>The number of raw logs that can be downloaded at a time is increased from 10 million to 50 million, and the limit on the number of download tasks is removed, significantly improving the log download speed.</td><td>2021-11-08</td><td><a href="https://intl.cloud.tencent.com/document/product/614/34234">Downloading Log</a></td></tr>
	</tbody>
</table>

## October 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Support for template variables in the dashboard</td><td>The data source variable and quick filter variable are added to the dashboard, allowing you to flexibly switch between log topics for multiple data sources in the same dashboard and quickly filter metric conditions.</td><td>2021-10-19</td><td><a href="https://intl.cloud.tencent.com/document/product/614/43561">Template Variable</a></td></tr>
	</tbody>
</table>


## September 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Kafka real-time consumption</td><td>The Kafka consumption capability is now available in CLS. You can use the Kafka real-time consumption feature to export log data to specified applications efficiently and conveniently.</td><td>2021-09-17</td><td><a href="https://intl.cloud.tencent.com/document/product/614/47570">	Kafka Real-time Consumption</a></td></tr>
	</tbody>
</table>


## August 2021
<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Brand-new monitoring alarm features</td><td>	
Updated features:<ul  style="margin: 0;"><li>Added custom alarm content templates</li><li>Added the custom multi-dimensional analysis feature</li><li>Added the feature of reporting alarms within one minute when exceptions occur</li></ul></td><td>2021-08-22</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39573">Monitoring Alarm Overview</a></td></tr>
		<tr><td>Offline log solution in beta testing</td><td>Adopted the low-cost offline log storage solution to search and store massive infrequently accessed logs, requiring a total cost 80% lower than that of <B>real-time log storage</B>. The solution is now available in Beijing, Shanghai, Guangzhou, Nanjing, Chongqing, and Hong Kong, China.</td><td>2021-08-18</td><td><a href="https://intl.cloud.tencent.com/document/product/614/42004">Offline Storage Overview</a></td></tr>
		<tr><td>Released over 200 analytic functions</td><td>Over 200 SQL analytic functions are released in all regions to meet log data aggregate analysis in various scenarios to enhance CLS's data visualization capability.</td><td>2021-08-12</td><td><a href="https://www.tencentcloud.com/document/product/614/36745">SQL Functions</a></td></tr>
		<tr><td>Log parsing based on custom formats</td><td>Added the LogListener advanced data processing feature to allow users to parse log files based on custom formats to implement the collection of logs in complex formats.</td><td>2021-08-06</td><td><a href="https://intl.cloud.tencent.com/document/product/614/42742">Custom Format</a></td></tr>
	</tbody>
</table>

## July 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Full/Incremental collection policies</td><td>Added the feature to allow users to configure whether to use full or incremental log collection via LogListener, meeting users' requirement for shipping only new log data and significantly reducing users' write traffic costs.</td><td>2021-07-22</td><td><a href="https://intl.cloud.tencent.com/document/product/614/32287">Full/Incremental Collection Policy</a></td></tr>
		<tr><td>Optimized search error messages</td><td>Standardized error messages for higher readability of the search error information.</td><td>2021-07-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/44224">Search Analysis Error</a></td></tr>
		<tr><td>Chinese text segmentation</td><td>Added the Chinese text segmentation feature to segment logs containing Chinese characters based on the Chinese syntax to facilitate log search.</td><td>2021-07-08</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39594">Chinese Text Segmentation</a></td></tr>
	</tbody>
</table>


## June 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Deploying LogListener instances on CVM instances in batches</td><td>Added the feature to allow users to deploy LogListener instances on CVM instances in batches for CVM log collection. With the feature, users do not need to manually install LogListener configuration anymore.</td><td>2021-06-24</td><td>-</td></tr>
		<tr><td>Map, Sankey, and other chart features released</td><td>Added the support for more data visualization charts, including bar charts, column charts, maps, and Sankey diagrams.</td><td>2021-06-18</td><td>-</td></tr>
		<tr><td>Search statement syntax error correction prompts</td><td>Added search syntax error prompts for the correction of Lucene syntax errors and spelling errors in index statistics fields, effectively improving the accuracy and efficiency of users' search analysis statements.</td><td>2021-06-15</td><td>-</td></tr>
	</tbody>
</table>


## May 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Dashboard 2.0 release</td><td>Released dashboard 2.0 UI: enhanced visualization and optimized the dashboard style.</td><td>2021-05-31</td><td>-</td></tr>
		<tr><td>LogListener download over a private network</td><td>Added the support for users to download the LogListener installation package via a private network address in different regions, avoiding security risks caused by connecting to a public network.</td><td>2021-05-27</td><td><a href="https://intl.cloud.tencent.com/document/product/614/17414">LogListener Installation Guide</a></td></tr>
		<tr><td>Log topic traffic statistics</td><td>Added the feature of monitoring the traffic statistics of a single log topic, allowing users to view the traffic dynamics of a log topic.</td><td>2021-05-20</td><td>-</td></tr>
		<tr><td>Collection configuration import</td><td>Added the feature of importing existing log topic rules with a few clicks, improving log data access efficiency.</td><td>2021-05-17</td><td><a href="https://intl.cloud.tencent.com/document/product/614/40863">Importing LogListener Collection Configuration</a></td></tr>
	</tbody>
</table>

## April 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>LogListener service log launch</td><td>Added the support for LogListener service logs. These logs record LogListener running status and collection monitoring log data. The logs are presented in a visualized view to provide important metric data.</td><td>2021-04-26</td><td><a href="https://intl.cloud.tencent.com/document/product/614/40232">LogListener Service Logs</a></td></tr>
	</tbody>
</table>

## March 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Uploading parsing-failure logs</td><td>Added the support for uploading parsing-failure logs, using `LogParseFailure` as the key name (`Key`) and the raw log content as the key value (`Value`).</td><td>2021-03-26</td><td>-</td></tr>
		<tr><td>CLS newly available in Moscow and Thailand</td><td>CLS is now available in Moscow in Europe and Bangkok in Asia Pacific.</td><td>2021-03-20</td><td><a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a></td></tr>
	</tbody>
</table>

## February 2021

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>LogListener auto upgrade</td><td>Users can set a time period for agent auto upgrade or select specific machines to upgrade manually.</td><td>2021-02-27</td><td><a href="https://intl.cloud.tencent.com/document/product/614/40233">LogListener Upgrade Guide</a></td></tr>
		<tr><td>Millisecond-precision logging</td><td>LogListener supports millisecond-precision timestamps for log collection. After time-based log collection is enabled, LogListener uploads logs with millisecond-precision UNIX timestamps.</td><td>2021-02-20</td><td>-</td></tr>
		<tr><td>Supported downloading millions of logs</td><td>CLS allows users to download up to millions of logs. Users can specify the quantity of logs they want to export by setting search criteria and time range. Logs can be exported in two formats: CSV and JSON. </td><td>2021-02-14</td><td><a href="https://intl.cloud.tencent.com/document/product/614/34234">Downloading Log</a></td></tr>
		<tr><td>Context search</td><td><ul  style="margin: 0;"><li>Added the feature for locating the current log, allowing users to quickly locate a target log and scroll to view the log context.</li><li>Added the feature to highlight a number of strings, quickly marking the keywords that users use to search.</li><li>Added the filter condition feature to allow users to quickly locate the log where a target character string resides. </li></ul></td><td>2021-02-06</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39795">Context Search and Analysis</a></td></tr>
	</tbody>
</table>

## December 2020

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Monitoring Alarm 2.0 release</td><td>CLS allows users to set alarm policies for log topics. When query and analysis results meet the trigger conditions specified, the users can receive alarm notifications and they can monitor the log data in real time. </td><td>2020-12-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39573">Monitoring Alarm Overview</a></td></tr>
		<tr><td>CLS connection to Grafana</td><td>CLS can be connected to Grafana to export CLS's raw log data and SQL aggregate analysis results for display in Grafana.</td><td>2020-12-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39592">CLS Connection to Grafana</a></td></tr>
		<tr><td>Supported extracting multi-line logs with a regular expression</td><td>The extraction mode of <b>multi-line - full regular expression</b> is added to LogListener collection configuration rules for log collection.</td><td>2020-12-15</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39590">Full Regular Expression (Multi-Line)</a></td></tr>
		<tr><td>Released Search Page 2.0</td><td><ul  style="margin: 0;"><li>The time component supports millisecond precision, and a <b>custom time<b> can be input quickly, improving query efficiency.</li><li>The <b>original layout and table layout<b> and <b>whether to turn on line break<b> features are added to log data display, enabling flexible switching.</li><li>Preference settings are added to allow users to customize the <b>number of logs for loading<b> and the <b>number of historical records<b>, meeting diversified data browsing needs.</li></ul></td><td>2020-12-15</td><td>-</td></tr>
	</tbody>
</table>

## November 2020

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>SQL statistical analysis fully available</td><td>CLS provides the SQL statistical analysis feature to help users aggregate and analyze log data and display the analysis results in charts. </td><td>2020-11-24</td><td><a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td></tr>
		<tr><td>Supported shipping to SCF</td><td>CLS supports shipping data of log topics to SCF via the CLS's log trigger to meet log data ETL requirements. </td><td>2020-11-20</td><td><a href="https://www.tencentcloud.com/document/product/614/38883">Overview</a></td></tr>
		<tr><td>CLS working with TKE (event and audit center)</td><td>CLS and TKE jointly launched the cluster audit and event log center, which allows users to view audit logs and cluster events in real time through visual charts, improving the efficiency of container cluster OPS with ease. </td><td>2020-11-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38338">Cluster Audit</a></td></tr>
	</tbody>
</table>

## October 2020

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>Automatically splitting topic partitions</td><td>After the auto-split feature is enabled, CLS will automatically split a topic partition into a reasonable number of partitions based on the actual write situation if the topic partition continues to reach the corresponding write request or write traffic threshold.</td><td>2020-10-25</td><td><a href="https://intl.cloud.tencent.com/document/product/614/39587">Splitting Topic Partition</a></td></tr>
		<tr><td>Quick Field Analysis 2.0</td><td>Rebuilt version of quick field analysis:<ul  style="margin: 0;"><li>Users can view field statistics results more conveniently and quickly.</li><li>Users can quickly modify and save display fields.</li><li>Users can quickly change the display order of fields by dragging and dropping fields.</li></ul></td><td>2020-10-15</td><td>-</td></tr>
	</tbody>
</table>

## September 2020

<table>
	<thead>
		<tr>
			<th width="20%">Update</th>
			<th width="50%">Description</th>
			<th width="15%">Release Date</th>
			<th width="15%">Documentation</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>CLS newly available in Taipei and Seoul</td><td>CLS is now available in Taipei and Seoul.</td><td>2020-09-27</td><td><a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a></td></tr>
		<tr><td>Search page supporting layout configuration</td><td>The search page provides access for LogListener collection configuration and index configuration. It allows users to quickly view server group status and index field information.</td><td>2020-09-24</td><td>-</td></tr>
		<tr><td>Full support for Lucene syntax</td><td>CLS fully supports Lucene syntax search.</td><td>2020-09-18</td><td><a href="https://intl.cloud.tencent.com/document/product/614/37803">Syntax and Rules</a></td></tr>
		<tr><td>Release of free tiers</td><td>After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region.</td><td>2020-09-12</td><td><a href="https://www.tencentcloud.com/document/product/614/37508">Purchase Guide</a></td></tr>
	</tbody>
</table>

