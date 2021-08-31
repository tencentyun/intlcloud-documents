
## Billing Overview

Tencent Cloud provides high-quality multi-line BGP networks to ensure an optimal network experience.
Tencent Cloud currently provides two billing plans: bill-by-traffic and bill-by-bandwidth.
>! 
> - The public network fee is billed based on outbound bandwidth/traffic. The outbound bandwidth refers to the bandwidth from the CVM to the public network. For example, the user uses the client to download CVM instance resources.
> - To avoid unexpected costs due to traffic surges, you can set a bandwidth cap. Any traffic over the cap will be dropped and will not incur any costs.
> 


## Billing Plans


The following tables compare the payment methods, billing cycles, and use cases of the two different billing plans:

- Calculating usage based on traffic (GB):

 <table class="comparison-table">
                     <tbody><tr>
                        <th>Billing Plan</th>
                        <th>Payment Method</th>
                                    <th>Billing Cycle</th>
<th>Use Cases</th>
                     </tr>
                     <tr>
                        <td>By traffic</td>
                        <td>Postpaid</td> 
                                    <td>Hourly</td>
                                    <td>Suitable for scenarios where the peak business traffic fluctuates greatly at varying times.</td></tr></tbody></table>

- Calculating usage based on bandwidth (Mbps):


 <table class="comparison-table">
                     <tbody><tr>
                        <th>Billing Plan</th>
                        <th>Payment Method</th>
                                    <th>Billing Cycle</th>
<th>Use Cases</th>
                     </tr>
                        <td>Bandwidth packages</td>
                        <td>Postpaid</td> 
                                    <td>Monthly</td>
                                    <td>Suitable for large-scale businesses where traffic can be staggered between different instances using the public network.</td>
</tr></tbody></table>


- The peak bandwidths of the bill-by-traffic billing plan and the bill-by-bandwidth billing plan are different. See the table below for details.
<table>
       <tbody><tr>
            <th>Bill-by-traffic</th>
            <th>Bill-by-bandwidth</th>
       </tr>
       <tr>          
            <td>The peak bandwidth is only regarded as the <strong>maximum peak bandwidth</strong>, and not as the fixed bandwidth. In case of resource contention, the peak bandwidth may be limited.</td> 
            <td>The peak bandwidth is regarded as the fixed bandwidth. In case of resource contention, the peak bandwidth will be guaranteed and will not be limited.</td>
            </tr> 
</tbody></table>

## Documentation
[Public Network Fee](https://intl.cloud.tencent.com/zh/document/product/213/39743)



