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
<td>Maximum code size (including bound layers) per function (version) before compression</td>
<td>500 MB</td>
</tr>
<tr>
<td>Maximum number of triggers per function</td>
<td>10</td>
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
>- SCF currently supports 10,000-level concurrency, which can effectively support scenarios with high concurrency demand such as ecommerce promotions and parallel processing of medical and biological data.
>- The concurrency quota per region on the SCF platform is shared by all functions by default. You can [customize the concurrency for specific functions](https://intl.cloud.tencent.com/document/product/583/37040) to meet your actual needs. To request an increase in the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) to apply.
> - In SCF, a [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707) has limits in two dimensions: SCF and COS, as detailed below:
>  - SCF dimension: one function can be bound to 10 COS triggers at most. 
>  - COS dimension: the same event and prefix/suffix rule of one function can trigger up to 3 functions, and one COS bucket can be bound to 10 rules at most.



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

>! If the size of a Base64-encoded file is below 6 MB, you can pass the encoded file to SCF through [API Gateway](https://intl.cloud.tencent.com/zh/product/apigateway). Otherwise, we recommend you upload the file to [COS](https://intl.cloud.tencent.com/zh/product/cos) and pass the object address to SCF first. Then, SCF will pull the file from COS to complete the upload.

