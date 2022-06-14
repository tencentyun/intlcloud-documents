[Elastic Network Interface](https://intl.cloud.tencent.com/products/eni) (ENI) is an elastic network interface bound to CVMs in a VPC, which can be migrated among multiple CVMs. ENI is very useful for configuring management networks and establishing highly reliable network solutions.

ENI has VPC, availability zone and subnet attributes. You can only bind it to CVMs under the same availability zone. A CVM can be bound with multiple ENIs, and the maximum number allowed varies by CVM specifications.

## Concepts

 - **Primary ENI and secondary ENI:** The ENI created when creating the CVM in a VPC is the primary ENI, and those created by users are secondary ENIs. The primary ENI does not support binding and unbinding, but secondary ENIs do.
 - **Primary private IP:** The primary private IP of an ENI is randomly assigned by the system or customized by users when the ENI is created. You can modify the primary private IP of the primary ENI, but not those of secondary ENIs.
 - **Secondary private IP:** The secondary private IPs bound to the ENI, other than the primary IP, are configured by users when they create or modify the ENI. Users can also bind/unbind these IPs.
 - **EIP:** Bound with private IPs of an ENI one by one.
 - **Security group:** An ENI can be bound with one or more security groups.
 - **MAC address:** An ENI has a globally unique MAC address.

## Applications
- **Isolation among private network, public network and management network**:
Isolation among private network, public network and management network for secure data transmission is required for the network deployment of key businesses. Different routing policies and security group policies can guarantee data security and network isolation. Like a physical server, CVM can be bound with ENIs residing in different subnets to achieve isolation among three networks.
- **Highly reliable application deployment:**
The high availability of key components in the system architecture is ensured through multi-server hot backup. Tencent Cloud provides ENIs and private IPs that can be flexibly bound and unbound. You can configure Keepalived disaster recovery to achieve highly available deployment of key components.

## Limits

Based on CPU and memory configurations, the number of ENIs bound to a CVM differs from the number of private IPs bound to an ENI. The quotes are as shown below:


<dx-alert infotype="notice" title="">
The number of IPs that can be bound to a single ENI indicates the upper limit of IPs bound only. The EIP use limits, rather than the upper limit, determines the actual EIP quota.
</dx-alert>


<dx-tabs>
::: Number of ENIs bound to a CVM instance
<table>
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
    <th style="text-align:center">Standard S5</th>
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
    <th rowspan="5" style = "text-align:center;">MEM Optimized</th>
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
    <td >8</td>
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
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine 2.0</th>
    <td colspan="10" style = "text-align:center;">Not supported</td>
   </tr>
  </table>
:::
::: Number of private IPs bound to a single ENI on CVM instances
<table>
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Model</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Instance Type</th>
    <th width="86%" colspan="10" style = "text-align:center;">Number of private IPs bound to a single ENI</th>
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
    <th style="text-align:center">Standard S5</th>
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
    <th rowspan="5" style = "text-align:center;">MEM Optimized</th>
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
    <td  >30</td>
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
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine 2.0</th>
    <td colspan="10" style = "text-align:center;">Not supported</td>
   </tr>
  </table>
:::
</dx-tabs>

## API Overview
The APIs related to the ENI and CVM are shown in the following table. For more information, see [API Category](https://intl.cloud.tencent.com/document/product/215/15755).

| Feature | Action ID | Description |
|---------|---------|---------|
| Create ENI | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818) | Create an ENI |
| Assign Private IP for ENI | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813) | Assign a private IP for an ENI |
| Bind ENI to CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819) | Bind an ENI to a CVM |
