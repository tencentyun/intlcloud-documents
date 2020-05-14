The access logs of CLB collect and record the details of each client request, such as the request time, request path, client IP and port, return code, and response time, which can help you better understand client requests, troubleshoot issues, and analyze user behaviors.
>
>- The feature of storing access logs in COS will stop accepting new enablement requests after 00:00:00, May 15, 2020 (00:00:00, April 26, 2020 for the Guangzhou region) and will be officially disused after 00:00:00, June 30, 2020. Please use the upgraded feature of [storing access logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063).
>- Access logs can be configured only for layer-7 CLB but not layer-4 CLB.
>- Currently, access logs can only be configured in certain regions. For more information, please see below.

## Storage Methods
There are two methods for storing the access logs of CLB:
- [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): CLS is a one-stop log service platform that provides a wide variety of log services such as log collection, storage, search, analysis, real-time consumption, and shipping. It assists you in implementing business operations, security monitoring, log auditing, and log analysis.
- [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436): COS is a distributed storage service designed to store a high number of files. You can easily and quickly access it to upload, download, and manage files in various formats for storage and management of massive amounts of data.


<table class="table"><thead><tr><th>Item</th><th>Storing Access Logs to CLS</th><th>Storing Access Logs to COS</th></tr></thead>
<tbody><tr><td>Time granularity for getting logs</td><td> Minute</td><td>Hour</td></tr>
<tr><td>Online search</td><td>Supported</td><td>Not supported. You must download an access log for data search</td></tr>
<tr><td>Search syntax</td><td>Full-text search, key-value search, fuzzy keyword search, etc. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/614/30439">Search Rules</a></td><td>Typically full-text search</td></tr>
<tr><td>Supported regions</td><td>It is supported in Guangzhou, Chengdu, and Toronto and currently in beta test in Shanghai, Nanjing, Beijing, Chongqing, Hong Kong (China), Silicon Valley, and Singapore. To try it out, please submit a <a href="https://console.cloud.tencent.com/workorder/category">ticket</a> for application </td><td>Guangzhou, Shanghai, Beijing, Hong Kong (China). Shanghai Finance, and Shenzhen Finance</td></tr>
<tr><td>Supported types</td><td>Public network/private network CLB</td><td>Public network CLB</td></tr>
</tbody></table>

## Related Operations
- [Storing Access Logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063)
- [Storing Access Logs in COS](https://intl.cloud.tencent.com/document/product/214/10329)
