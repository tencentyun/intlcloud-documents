The price of a CVM instance consists of hardware (CPUs and memory), disk (system disks and data disks), and network fees. When you purchase a CVM instance, the corresponding resources are available on the purchase page. This document describes the pricing, purchase method, and configuration modification of CVM instance hardware (CPUs and memory).

## Prices for Pay-as-You-Go Instances


<dx-alert infotype="explain" title="">
This section describes the pricing rules for pay-as-you-go CVM instances. Please use [CVM Price Calculator](https://intl.cloud.tencent.com/pricing/cvm/calculator) to check out the price details.
</dx-alert>

Some CVM instance types are billed on a pay-as-you-go basis with 3-tiered pricing. For instance types that support 3-tiered pricing, newly purchased instances, and CVM instances where the original configuration remains unchanged are billed based on 3-tiered pricing. For details about instance types that support and do not support 3-tiered pricing, see the tiered pricing details on the purchase page.


### Notes

<ul>
<li>The list prices of pay-as-you-go instances is at an hourly rate. They are billed per second on an hourly billing cycle.</li>
<li>The CVM tiered pricing policy applies only to the CPU and memory fees.</li>
<li>The price calculator displays the tier-1 price.
	<ul>
		<li><b>For instance types that support 3-tiered pricing: </b>Tier-2 price = Tier-1 price x 50%; Tier-3 price = Tier-1 price x 34%</li>
		<li><b>For instance types that do not support 3-tiered pricing: </b>Tier-1 price = Tier-2 price = Tier-3 price</li>
	</ul>
	For details about instance types that support and do not support tiered pricing, see the tiered pricing details on the purchase page or pricing center.
</li>
<li>The tiered pricing policy applies only to CVMs with unchanged configurations. If the configuration of a CVM is changed, the CVM is thereafter billed based on the tier-1 price of the new configuration.
<br>For example, the original configuration of a CVM is 2C4G. When the CVM is used for 100 hours, it enters the tier-2 pricing phase. If the configuration is changed to 1C2G at this time, the CVM is billed based on the tier-1 pricing of 1C2G.
</li>
<li>The overdue payment policy for pay-as-you-go CVMs remains unchanged. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/2181">Overdue payment policy</a>.</li>
<li>Discounts are not provided for pay-as-you-go CVMs.</li>
<li>Eligible pay-as-you-go instances (CPU and memory) are not charged after shutdown. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/19918">No Charges When Shut Down for Pay-as-You-Go Instances</a>.</li>
During the No Charges When Shut Down period, pay-as-you-go instances support for the tiered pricing no longer calculate the usage period. After the instance is restarted, its usage period will continue to count.
<li>Ineligible instances will still be charged after shutdown.</li>
</ul>
