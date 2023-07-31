CLB supports configuring access logs to collect and record the details of each client request, such as the request time, request path, client IP and port, return code, and response time. This feature can help you better understand client requests, troubleshoot issues, and analyze user behaviors.
>?
>- Only Layer-7 CLB supports configuring access logs.
>- This feature is only available in regions listed below.

## Storage Methods
- CLB access logs can be stored in [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): CLS is a one-stop log service platform that provides a variety of log services including log collection, storage, search, analysis, real-time export, and shipping. It assists you in implementing business operations, security monitoring, log audit, and log analysis.

<table class="table">
<thead>
<tr>
<th>Item</th>
<th>Storing Access Logs in CLS</th>
</tr>
</thead>
<tbody>
<tr>
<td>Time granularity for log obtainment</td>
<td>Minute</td>
</tr>
<tr>
<td>Online search</td>
<td>Supported</td>
</tr>
<tr>
<td>Search syntax</td>
<td>Full-text search, key-value search, fuzzy keyword search, etc. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/614/37882">Legacy CLS Search Syntax</a>.</td>
</tr>
<tr>
<td>Supported regions</td>
<td>For more details on CLS available regions, see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a>.</td>
</tr>
<tr>
<td>Supported CLB type</td>
<td>Public network/private network CLB</td>
</tr>
<tr>
<td>Upstream and downstream links</td>
<td>CLS logs can be shipped to COS, and exported to CKafka for further processing.</td>
</tr> 
<tr>
<td>Log retention </td>
<td>Tencent Cloud does not store access logs by default. The storage feature can be configured as needed.</td>
</tr>
</tbody></table>

## Relevant Operations
- [Storing Access Logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063)
