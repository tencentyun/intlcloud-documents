The access logs of CLB collect and record the details of each client request, such as the request time, request path, client IP and port, return code, and response time, which can help you better understand client requests, troubleshoot issues, and analyze user behaviors.
>
>- The feature of storing access logs in COS will stop accepting new enablement requests after 00:00:00, May 15, 2020 (00:00:00, April 26, 2020 for the Guangzhou region) and will be officially disused after 00:00:00, June 30, 2020. For more information, please see [Announcement on the Deactivation of the Feature of Storing CLB Access Logs in COS](https://intl.cloud.tencent.com/document/product/214/35906). Please use the upgraded feature of [storing access logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063).
>- Access logs can be configured only for layer-7 CLB but not layer-4 CLB.
>- Currently, access logs can only be configured in certain regions. For more information, please see below.

## Storage Methods
There are two methods for storing the access logs of CLB:
- [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): CLS is a one-stop log service platform that provides a wide variety of log services such as log collection, storage, search, analysis, real-time consumption, and shipping. It assists you in implementing business operations, security monitoring, log auditing, and log analysis.
- [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436): COS is a distributed storage service designed to store a high number of files. You can easily and quickly access it to upload, download, and manage files in various formats for storage and management of massive amounts of data.


<table class="table"><thead><tr><th>Item</th><th>Storing Access Logs in CLS</th><th>Storing Access Logs in COS</th></tr></thead>
<tbody><tr><td>Time granularity for getting logs</td><td> Minute</td><td>Hour</td></tr>
<tr><td>Online search</td><td>Supported</td><td>Not supported. You must download an access log for data search</td></tr>
<tr><td>Search syntax</td><td>Full-text search, key-value search, fuzzy keyword search, etc. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/614/30439">Search Rules</a></td><td>Typically full-text search</td></tr>
<tr><td>Supported regions</td><td>It is supported in Guangzhou, Shanghai, Chengdu, Hong Kong (China), Nanjing, Beijing, Chongqing, Singapore, Mumbai,  Silicon Valley, and Frankfurt.  </td><td>Guangzhou, Shanghai, Beijing, Hong Kong (China)</td></tr>
<tr><td>Supported types</td><td>Public network/private network CLB</td><td>Public network CLB</td></tr>
<tr><td>Upstream and downstream links </td><td>CLS logs can be stored in COS, and consumed using CKafka</td><td>-</td></tr> 
<tr><td>Log Retention </td><td>Tencent Cloud stores no access log by default.  You need to store the access log in CLS as needed.</td><td>Tencent Cloud will retain the logs for three days by default in the regions that support storing access logs in COS.</td></tr>
</tbody></table>

## Relevant Operations
- [Storing Access Logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063)
- [Storing Access Logs in COS](https://intl.cloud.tencent.com/document/product/214/10329)
