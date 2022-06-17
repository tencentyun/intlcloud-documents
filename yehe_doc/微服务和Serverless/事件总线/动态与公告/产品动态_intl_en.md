## April 2022

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
<td>Releases the linkage tracing feature</td>
<td>The linkage tracing feature is added to EventBridge. For each event published to the event bus, a full-linkage processing log is reported, which makes each event traceable and improves product observability.
</td><td>2022-04-14</td><td>
<a href="https://intl.cloud.tencent.com/document/product/1108/46990">Linkage Tracing</a>
</td>
</tr>
<tr>
<td>Supports DTS event sources</td>
<td>DTS event sources are integrated into EventBridge. DML and DDL operations on upstream databases such as MySQL, TDSQL, and MariaDB can be synced to EventBridge in real time. Then these database operations are distributed to downstream targets such as computing and storage entities for processing.</td><td>2022-04-07</td><td>
<a href="https://intl.cloud.tencent.com/document/product/1108/46991">Configuring a DTS Connector</a>
</td>
</tr>
</tbody></table>


## March 2022

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
<td>Releases the ETL data conversion capability</td>
<td>The ETL capability is integrated into EventBridge. With the capability, EventBridge can directly cleanse, filter, associate, and convert data passed into EventBridge data sources in real time to create unified structured data and deliver the data to specified targets, implementing the fusion of different types of data from various data sources.
</td><td>2022-03-16</td><td>
<a href="https://intl.cloud.tencent.com/document/product/1108/46247">Configuring Data Conversion</a>
</td>
</tr>
</tbody></table>


## February 2022

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
<td>Supports CKafka event targets</td>
<td>CKafka event targets are added to EventBridge. Compared with the previous scheme of transferring events to CKafka by using SCF templates, this feature shortens the call linkage in the CKafka transfer scenario and significantly improves the architecture performance and processing efficiency.
</td><td>2022-02-28</td><td>
<a href="https://intl.cloud.tencent.com/document/product/1108/46249">CKafka Target</a>
</td>
</tr>
<tr>
<td>Integrates CloudAudit event sources</td>
<td>CloudAudit event sources are integrated into EventBridge. Operation logs of more than 100 Tencent Cloud services can be delivered to EventBridge. Then EventBridge filters the operation logs based on rules and delivers them to specified targets for processing, implementing automated Ops of business events on the cloud.
</td><td>2022-02-15</td><td>
<a href="https://intl.cloud.tencent.com/document/product/1108/46246">CloudAudit Event</a>
</td>
</tr>
</tbody></table>
