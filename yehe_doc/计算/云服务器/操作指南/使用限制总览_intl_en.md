## Account-level Limits for Purchasing CVM Instances

- You need to sign up for a Tencent Cloud account. For more information, see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
- If you create a pay-as-you-go CVM, the system will freeze the cost of one-hour CVM usage. Make sure that your account has sufficient balance for the order.


## CVM Instance Use Limits

- Virtualized software cannot be installed or re-virtualized (such as installing VMware or Hyper-V).
- You cannot use sound cards or mount external hardware devices (such as USB flash drives, external disks, and U-keys).
- Only Linux CVMs can act as a public gateway.

## CVM Instance Purchase Limits

- The **purchase limit** of pay-as-you-go CVM instances for each user in each AZ is between 30 and 60. 
- For more information, see [Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664).


## Image Limits

- Public images: No use limits.
- Custom images: Each region supports a maximum of 10 custom images.
- Shared images: Each custom image can be shared with a maximum of 50 Tencent Cloud users. Custom images can only be shared with accounts in the same region as the source account.
- For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).


## ENI Limits

Based on CPU and memory configurations, the number of ENIs bound to a CVM instance differs from the number of private IPs bound to an ENI. The quotes are as shown below:
>! The number of IP addresses bound to a single ENI indicates the maximum number allowed. The EIP quota is not provided based on this upper limit but based on EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

<dx-tabs>
::: ENIs per CVM instance
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Model</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Instance Type</th>
    <th width="86%" colspan="10" style = "text-align:center;">Number of ENIs</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 core</th>
    <th style = "text-align:center;">CPU: 2 cores</th>
    <th style = "text-align:center;">CPU: 4 cores</th>
    <th style = "text-align:center;">CPU: 6 cores</th>
    <th style = "text-align:center;">CPU: 8 cores</th>
    <th style = "text-align:center;">CPU: 10 cores</th>
    <th style = "text-align:center;">CPU: 12 cores</th>
    <th style = "text-align:center;">CPU: 14 cores</th>
    <th style = "text-align:center;">CPU: 16 cores</th>
    <th style = "text-align:center;">CPU: &gt;16 cores</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Standard</th>
    <th style = "text-align:center;">Standard S5</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard Storage Optimized S5se</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard SA2</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S4</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">Standard Network-optimized SN3ne</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S3</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard SA1</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S2</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">High IO</th>
    <th style = "text-align:center;">High IO IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">High IO IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">Memory Optimized</th>
    <th  style = "text-align:center;">Memory Optimized M5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Memory Optimized M4</th>
    <td >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Compute</th>
    <th  style = "text-align:center;">Compute Optimized C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Compute Network-optimized CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Compute C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Compute C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="6" style = "text-align:center;">GPU-based</th>
     <th class="xl71" x:str style = "text-align:center;">GPU Compute GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU Compute GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU Compute GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA-based</th>
    <th style = "text-align:center;">FPGA Accelerated FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big Data</th>
    <th  style = "text-align:center;">Big Data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">CPM</th>
    <td colspan="10" style = "text-align:center;">Not supported</td>
   </tr>
  </table>
:::
::: Private IPs per ENI
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Model</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Instance Type</th>
    <th width="86%" colspan="10" style = "text-align:center;">Private IPs bound to a single ENI</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 core</th>
    <th style = "text-align:center;">CPU: 2 cores</th>
    <th style = "text-align:center;">CPU: 4 cores</th>
    <th style = "text-align:center;">CPU: 6 cores</th>
    <th style = "text-align:center;">CPU: 8 cores</th>
    <th style = "text-align:center;">CPU: 10 cores</th>
    <th style = "text-align:center;">CPU: 12 cores</th>
    <th style = "text-align:center;">CPU: 14 cores</th>
    <th style = "text-align:center;">CPU: 16 cores</th>
    <th style = "text-align:center;">CPU: &gt;16 cores</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Standard</th>
    <th style = "text-align:center;">Standard S5</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard Storage Optimized S5se</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard SA2</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S4</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">Standard Network-optimized SN3ne</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S3</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard SA1</th>
    <td >1 GB memory: 2<br/>&gt;1 GB memory: 6</td>
    <td >10</td>
    <td >8 GB memory: 10<br/>16 GB memory: 20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S2</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Standard S1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">High IO</th>
    <th style = "text-align:center;">High IO IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">High IO IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">Memory Optimized</th>
    <th  style = "text-align:center;">Memory Optimized M5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Memory Optimized M4</th>
    <td >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memory Optimized M1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Compute</th>
    <th  style = "text-align:center;">Compute Optimized C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Compute Network-optimized CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Compute C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Compute C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">GPU-based</th>
    <th  style = "text-align:center;">GPU Compute GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">GPU Compute GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU Compute GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU Compute GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU Compute GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA-based</th>
    <th style = "text-align:center;">FPGA Accelerated FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big Data</th>
    <th  style = "text-align:center;">Big Data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">CPM</th>
    <td colspan="10" style = "text-align:center;">Not supported</td>
   </tr>
  </table>
:::
</dx-tabs>


## Bandwidth Limits

- Maximum outbound bandwidth (downstream bandwidth)
 - The following rules apply to instances created after 00:00, February 24, 2020:
<table>
<tr><th rowspan="2">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2">Maximum Bandwidth Range (Mbps)</th></tr>
<tr><th style="width: 18.5607%;">Instance Billing Method</th><th style="width: 24.5814%;">Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0-2000</td></tr>
</table>

 - The following rules apply to instances created before 00:00, February 24, 2020: 
<table>
<tr><th rowspan="2">Network Billing Method</th><th colspan="2">Instance</th><th rowspan="2">Range of Bandwidth Cap (Mbps)</th></tr>
<tr><th>Instance Billing Method</th><th>Instance Configuration</th></tr>
<tr><td>Bill-by-traffic</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bill-by-bandwidth</td><td>Pay-as-you-go instances</td><td>All</td><td>0-100</td></tr>
<tr><td>Bandwidth package</td><td colspan="2">All</td><td>0-2000</td></tr>
</table>


- Maximum inbound bandwidth (upstream bandwidth)
	- Purchased fixed bandwidth > 10 Mbps:Tencent Cloud will assign a public network inbound bandwidth equals to the purchased bandwidth.
	- Purchased fixed bandwidth < 10 Mbps, Tencent Cloud will assign 10-Mbps public network inbound bandwidth.

## Disk Limits

<table>
	<tr><th>Limitations</th><th>Description</th></tr>
	<tr><td>Elastic cloud disk capability</td><td>Starting from May 2018, all data disks purchased with CVM instances are elastic cloud disks, which can be unmounted from and remounted to CVM instances. This feature is supported in all <a href="https://intl.cloud.tencent.com/document/product/213/35071">availability zones</a>.</td></tr>
	<tr><td>Cloud disk performance</td><td>I/O specification applies to both input and output performance at the same time.</br>For example, if a 1-TB SSD has a maximum random IOPS of 26,000, it means that both its read and write performance can reach this value. Due to performance limits, if the block size in this example is 4 KB or 8 KB, the maximum IOPS can be reached. If the block size is 16 KB, the maximum IOPS cannot be reached (throughput has already reached the limit of 260 MB/s).</td></tr>
	<tr><td>Elastic cloud disks per CVM</td><td>A maximum of 20</td></tr>
	<tr><td>Snapshots per region</td><td>64 + Number of cloud disks in the region x 64</td></tr>
	<tr><td>Attaching cloud disks to a CVM</td><td>The CVM instance and cloud disks must be in the same availability zone.</td></tr>
	<tr><td>Snapshot rollback</td><td>Snapshot data can only be rolled back to the cloud disk where the snapshot was created.</td></tr>
	<tr><td>Creating cloud disks using snapshot - Type limit</td><td>Only snapshots of data disks can be used to create new elastic cloud disks.</td></tr>
	<tr><td>Creating cloud disks using snapshot - Size limit</td><td>The capacity of new cloud disk must be larger than the source disk of the snapshot.</td></tr>
</tr>
</table>



## Security Group Limits

- Security groups are region-specific. A CVM instance can only be bound to security groups in the same region.
- Security groups are applicable to CVM instances in any [network environment](https://intl.cloud.tencent.com/document/product/213/5227).
- Each user can configure a maximum of 50 security groups for each project in a region.
- A maximum of 100 inbound or outbound rules can be configured for a security group.
- One CVM instance can be associated with multiple security groups, and a security group can be associated with multiple CVM instances.
- Security groups associated with CVM instances on the **classic network** **cannot filter packets** from or to TencentDB (MySQL, MariaDB, SQL Server, or PostgreSQL) and NoSQL (Redis or Memcached) databases. Instead, you can use iptables or purchase CFW to filter traffic for such instances.
- The quotas are as shown below:
<table>
<tr><th>Item</th><th>Limit</th></tr>
<tr><td>Security groups</td><td>50 per region</td></tr>
<tr><td>Rules in a security group</td><td>100 for inbound rules and 100 for outbound rules</td></tr>
<tr><td>CVM instances associated with a security group</td><td>2,000</td></tr>
<tr><td>Security groups associated with a CVM instance</td><td>5</td></tr>
<tr><td>Security groups referenced by a security group</td><td>10</td></tr>
</table>

## VPC Limits

| Resource | Limit | 
|---------|---------|
| VPCs per region per account | 20 | 
| Subnets per VPC | 100 |
| Classic network-based CVMs associated with each VPC | 100 |
| Route tables per VPC | 10 |
| Route tables associated with each subnet | 1 |
| Routes per route table | 50 |
| HAVIPs per VPC | 10 |

