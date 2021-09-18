This document describes the use limits of AIA.

## Restrictions
- AIA only provides acceleration services for regions outside the Chinese mainland. It does not accelerate the transmission between the Chinese mainland and other regions.
- The Anycast EIP can be bound to a CVM instance, NAT Gateway, ENI, HAVIP, and private network CLB.
- When an Anycast EIP is created in the console, only one AIA BGP bandwidth package will be automatically created for each region. This bandwidth package only records the bandwidth usage details in the region, which is not used for billing.
- All Anycast EIPs in a single region are aggregated into the bandwidth package of the region, which is subdivided into bandwidth packages corresponding to the acceleration region. Assume you create an Anycast EIP in the Asia Pacific region (Hong Kong, China), the bill lists three bandwidth packages: Asia Pacific to Asia Pacific, Asia Pacific to North America, and Asia Pacific to Europe.


## Bandwidth Cap
The network bandwidth cap configured for an Anycast EIP refers to the maximum outbound bandwidth, i.e., the bandwidth flowing out from the Anycast EIP. The supported network bandwidth cap is 1-2000 (inclusive) Mbps.
>! An Anycast EIP created after July 20, 2021, 00:00:00 restricts the total outbound bandwidths of a single IP to the bandwidth cap. However, the bandwidth cap configured for Anycast EIPs created before the time point still restricts the maximum bandwidth going to a single region.

To restrict the total outbound bandwidths of an Anycast EIP created before July 20, 2021, you can adjust the bandwidth cap to apply the new rule. 


## Peak Bandwidth
<table>
<tr>
<th width="21%">Peak Bandwidth</th><th>Description</th>
</tr>
<tr>
<td>Single instance</td><td>The peak bandwidth of instances including public IP and EIP in a single bandwidth package is 2 Gbps. The peak bandwidth is only regarded as the maximum possible peak bandwidth, and not as the committed bandwidth. In case of resource contention, the peak bandwidth may not reach this value.</td>
</tr>
<tr>
<td>Single region</td><td>The sum of peak bandwidths of all the running instances billed on bandwidth packages cannot exceed 50 Gbps in one region. If your application requires a guaranteed or higher bandwidth, contact your sales rep or <a href="https://intl.cloud.tencent.com/contact-sales">contact us</a>.</td>
</tr>
</table>

## References
[Elastic IP (EIP)](https://intl.cloud.tencent.com/document/product/213/5733)

