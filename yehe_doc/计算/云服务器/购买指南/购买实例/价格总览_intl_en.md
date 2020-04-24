The price of a CVM instance consists of the hardware (CPUs and memory), disk (system and data disks), and network fees. When you purchase a CVM instance, corresponding resources are available on the purchase page. This document describes the pricing, purchase method, and configuration modification process of CVM instance hardware (CPUs and memory).


## Pricing for Pay-as-You-Go Instances

This section describes pricing rules for pay-as-you-go CVM instances.

Some types of CVM instances are billed on a pay-as-you-go basis with 3-tiered pricing. For instance types that support 3-tiered pricing, newly purchased instances and other CVM instances whose original configuration remains unchanged are billed based on 3-tiered pricing. For details on instance types that support or do not support 3-tiered pricing, see tiered pricing details on the purchase page.


### Notes

<ul>
<li>The billing unit is USD per hour.</li>
<li>The CVM tiered pricing policy applies only to the CPU and memory fees.</li>
<li>The price calculator displays the tier-1 price.
	<ul>
		<li><b>For instance types that support 3-tiered pricing:</b> Tier-2 price = Tier-1 price × 50%; Tier-3 price = Tier-1 price × 34%</li>
		<li><b>For instance types that do not support 3-tiered pricing:</b> Tier-1 price = Tier-2 price = Tier-3 price</li>
	</ul>
	For details on instance types that support or do not support tiered pricing, see tiered pricing details on the purchase page or in the pricing center.
</li>
<li>The tiered pricing policy applies only to CVMs with unchanged configurations. If the configuration of a CVM is changed, the CVM is thereafter billed based on the tier-1 price of the new configuration.
<br>For example, the original configuration of a CVM is 2 cores and 4-GB memory. When the CVM has been used for 100 hours, the pricing of the CVM switches to tier-2 pricing. If the configuration becomes 1 core and 2-GB memory, the CVM is thereafter billed based on the tier-1 price of 1 core and 2-GB memory.
</li>
<li>The arrears mechanism for pay-as-you-go CVMs remains unchanged. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/2181#.E6.8C.89.E9.87.8F.E8.AE.A1.E8.B4.B9.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8">Pay-as-You-Go CVM Arrears Reminder</a>.</li>
<li>Discounts are unavailable for pay-as-you-go CVMs.</li>
<li>Eligible pay-as-you-go instances (CPUs and memory) are not charged after shutdown. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/19918">Details on Zero Charges for Shut Down Pay-as-You-Go Instances</a>. Ineligible instances will still be charged after shutdown.
</ul>

