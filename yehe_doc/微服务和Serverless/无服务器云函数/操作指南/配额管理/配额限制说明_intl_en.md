SCF has certain quota limits for each user account.




### User Account Quota Limits

<table>
<thead>
<tr>
<th>Content</th>
<th>Default Quota Limit</th>
</tr>
</thead>
<tbody>
<tr>
<td>Total function code size per region</td>
<td>100 GB</td>
</tr>
<tr>
<td rowspan="2">Total function concurrency quota per region</td>
<td>128,000 MB<br>(Guangzhou, Shanghai, Beijing, Chengdu, and Hong Kong (China))</td></tr>
<tr><td>64,000 MB<br>(Mumbai, Singapore, Tokyo, Toronto, Silicon Valley, Frankfurt, Shenzhen Finance, and Shanghai Finance)</td>
</tr>
<tr>
<td>Number of namespaces per region</td>
<td>5</td>
</tr>
<td>Total concurrent function quota per namespace</td>
<td>You can purchase a <a href="https://console.cloud.tencent.com/scf/buy?rid=1&amp;ns=default">function package</a> to adjust the quota.</td>
</tr>
<tr>
<td>Number of functions per namespace</td>
<td>50</td>
</tr>
</tbody></table>

### Function Quota Limits

<table>
<thead>
<tr>
<th>Content</th>
<th>Default Quota Limit</th>
</tr>
</thead>
<tbody>
<tr>
<td>Function name length limit</td>
<td>60 characters. The total length of the namespace name + function name cannot exceed 118 characters.</td>
</tr>
<tr>
<td>Maximum code size (including bound layers) per function (version) before compression</td>
<td>500 MB</td>
</tr>
<tr>
<td>Maximum number of same-type triggers per function</td>
<td>10</td>
</tr>
<tr>
<td>Maximum environment variable size per function</td>
<td>4 KB</td>
</tr>
<tr>
<td>Number of layer versions bound to one function version</td>
<td>5</td>
</tr>
</tbody></table>


### Layer Quota Limits
<table>
<thead>
<tr>
<th>Content</th>
<th>Default Quota Limit</th>
</tr>
</thead>
<tbody>
<tr>
<td>Number of layers per region</td>
<td>20</td>
</tr>
<tr>
<td>Number of versions per layer</td>
<td>200</td>
</tr>
</tbody></table>

>! 
>- SCF currently supports one million MB-level concurrency, which can effectively support scenarios with high concurrency demand such as ecommerce promotions and parallel processing of medical and biological data.
>- The concurrency quota per region on the SCF platform is shared by all functions by default. You can customize the [function concurrency](https://intl.cloud.tencent.com/document/product/583/37040) to meet your actual needs. If you want to increase the quotas or add concurrency quota management capabilities at the namespace granularity, you can directly purchase a [function package](https://console.cloud.tencent.com/scf/buy?rid=1&ns=default).
> - In SCF, a [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707) has limits in two dimensions: SCF and COS, as detailed below:
>  - SCF dimension: One function can be bound to 10 COS triggers at most.   
>  - COS dimension: The same event and prefix/suffix rule of one COS bucket can be bound to only one function.



### Function Runtime Environment Limits

| Item | Quota Limit |
| -------------------------------- | --------------------------------------------------- |
| Allocated memory | Minimum: 64 MB, maximum: 3,072 MB, in increments of 128 MB starting from 128 MB |
| Temporary cache space; i.e., size of the `/tmp` directory | 512 MB |
| Timeout period | Minimum: 1 second, maximum: 900 seconds |
| Number of file descriptors | 1,024 |
| Total processes and threads | 1,024 |
| Sync request event size | 6 MB |
| Sync request response size | 6 MB |
| Async request event size | 128 KB |

>! If the size of a Base64-encoded file is below 6 MB, you can pass the encoded file to SCF through [API Gateway](https://intl.cloud.tencent.com/products/apigateway); otherwise, we recommend you upload the file to [COS](https://intl.cloud.tencent.com/products/cos) and pass the object address to SCF first. Then, SCF will pull the file from COS to complete the upload.

