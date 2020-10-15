
## Billing Overview

Tencent Cloud provides high-quality multi-line BGP networks to ensure an optimal network experience.
Tencent Cloud currently provides two billing plans: bill-by-traffic and bill-by-bandwidth.
>! 
> - Currently, the public network is billed based on outbound bandwidth/traffic. The outbound bandwidth refers to the bandwidth from the CVM to the public network. For example, the user uses the client to download CVM instance resources.
> - To avoid unexpected costs due to traffic surges, you can set a bandwidth cap. Any traffic over the cap will be dropped and will not incur any costs.
> 


## Billing Plans
>? Monthly subscription is currently in beta. This pricing document is for reference only, please see your bill for the actual price. If you wish to use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>

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
                        <td><a href="#1">Bill-by-traffic</a></td>
                        <td>Postpaid</td> 
                                    <td>Billed hourly</td>
                                    <td>Suitable for scenarios where the peak business traffic fluctuates greatly at varying times.</td></tr></tbody></table>

- Calculating usage based on bandwidth (Mbps):

 <table class="comparison-table">
                     <tbody><tr>
                        <th>Billing Plan</th>
                        <th>Payment Method</th>
                                    <th>Billing Cycle</th>
<th>Use Cases</th>
                     </tr>
                                     <tr>
                        <td><a href="#3">Monthly bandwidth subscription</a></td>
                        <td>Prepaid</td> 
                                    <td>Billed monthly</td>
                                    <td>Suitable for scenarios where the peak business traffic is stable and is used long-term.</td></tr>
                                    <tr>
                        <td><a href="#4">Bandwidth packages</a></td>
                        <td>Postpaid</td> 
                                    <td>Billed monthly</td>
                                    <td>Suitable for large-scale businesses where traffic can be staggered between different instances using the public network.</td></tr></tbody></table>


- The peak bandwidths of the bill-by-traffic billing plan and the bill-by-bandwidth billing plan are different. See the table below for details.
<table>
       <tbody><tr>
            <th>Bill-by-traffic</th>
            <th>Bill-by-bandwidth</th>
       </tr>
       <tr>          
            <td>The peak bandwidth is only regarded as the <strong>maximum peak bandwidth</strong>, and not as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth may be limited.</td> 
            <td>The peak bandwidth is regarded as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth will be guaranteed and will not be limited.</td>
            </tr> 
</tbody></table>


> ?Base conversion: 1 GB = 1,000 MB; 1 MB = 1,000 KB; 1 Gbps = 1,000 Mbps; 1 Mbps = 1,000 Kbps.
> 

<span id="1"></span>
### Bill-by-traffic

Fees are pay-as-you-go on an hourly billing cycle based on the public network traffic used. Bill-by-traffic is suitable for scenarios where the peak business traffic fluctuates greatly at varying times.

#### Pricing

<table>
<thead>
<tr>
<th>Region</th>
<th>Price (unit: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Chinese mainland, Seoul, Hong Kong (China), Singapore, Frankfurt</td>
<td>0.12</td>
</tr>
<tr>
<td>Toronto, Silicon Valley</td>
<td>0.077</td>
</tr>
<tr>
<td>Moscow, Tokyo</td>
<td>0.13</td>
</tr>
<tr>
<td>Virginia</td>
<td>0.075</td>
</tr>
<tr>
<td>Bangkok, Mumbai</td>
<td>0.1</td>
</tr>
</tbody></table>

#### Billing sample

Suppose a user with a bill-by-IP account purchases an EIP in Seoul region with the bill-by-traffic billing mode. If this user binds a CVM betwen 07:00:00 - 07:59:59 and uses 10 GB of traffic, the fees incurred within 07:00:00 - 07:59:59 will be: 0.12 USD/GB × 10 GB = 1.2 USD.

> ?Public network traffic is the traffic data based on the number of downstream bytes, which is the application-layer data. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, so the traffic counted by Tencent Cloud may be about 10% more than that counted by users themselves on the server.
>
> - Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes and includes TCP and IP headers of 40 bytes, which generate traffic during transfer but cannot be counted by the application layer. The overhead of this part is around 3%.
> - TCP retransmission: during normal data transfer over the network, around 3-10% of packets are lost on the Internet and retransmitted by the server. This type of traffic cannot be counted by the application layer and accounts for 3-7% of the total traffic.


<span id="Step 3"></span>
### Monthly bandwidth subscription

With monthly bandwidth subscription, you can purchase fixed bandwidth in advance according to your needs. The payment method is prepaid. Monthly bandwidth subscription is suitable for scenarios where the peak business traffic is stable and is used long-term.

>? Monthly subscription is currently in beta. If you wish to use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>

#### Pricing

<table>
<thead>
<tr>
<th rowspan="2" width="10%">Region</th>
<th colspan="3"  style="text-align:center;">Price (unit: USD/Mbps/month)</th>
</tr>
<tr>
<th>Bandwidth ≤ 2 Mbps</th>
<th>2 Mbps ＜ Bandwidth ≤ 5 Mbps</th>
<th>Bandwidth ＞ 5 Mbps</th>
</tr>
</thead>
<tbody><tr>
<td>Guangzhou<br>Qingyuan<br>Shanghai<br>Beijing<br>Hong Kong, China<br>Singapore</td>
<td>2.86   </td>
<td>3.57</td>
<td>12.86</td>
</tr>
<tr>
<td>Chengdu<br>Chongqing  </td>
<td>2.57</td>
<td>3.15</td>
<td rowspan="5">11.43</td>
</tr>
<tr>
<td>Toronto<br>Silicon Valley<br>Virginia<br>Bangkok<br>Mumbai<br>Moscow</td>
<td colspan="2">4.29   </td>
</tr>
<tr>
<td>Seoul<br>Frankfurt</td>
<td colspan="2">2.86</td>
</tr>
<tr>
<td>Tokyo</td>
<td colspan="2">3.57</td>
</tr>
</tbody></table>


#### Billing sample

Suppose a user with a bill-by-IP account purchases an EIP in Singapore region with the monthly bandwidth subscription billing mode. If this user purchases a fixed bandwidth of 15 Mbps for 2 months, the fees will be: (2.86 USD/Mbps/month × 2 Mbps + 3.57 USD/Mbps/month × 3 Mbps + 12.86 USD/Mbps/month × 10 Mbps) × 2 months = 290.06 USD.

<span id="Step4"></span>

### Bandwidth packages

EIP bandwidth package is a monthly pay-as-you-go service, which is suitable for large-scale businesses where traffic can be staggered between different instances using the public network. For details, please refer to [Billing Overview](https://intl.cloud.tencent.com/document/product/684/15255).






