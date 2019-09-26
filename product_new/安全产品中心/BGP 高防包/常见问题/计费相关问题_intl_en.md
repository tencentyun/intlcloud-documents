## Does the same billing mode apply to the Anti-DDoS Pro elastic protection services? How is it calculated?
Yes, it does. The elastic protection services are also charged based on the elastic protection bandwidth range corresponding to the daily maximum protected attack traffic bandwidth. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747).
For example, assume that you have purchased an Anti-DDoS Pro instance with 20 Gbps base protection bandwidth + 50 Gbps elastic protection bandwidth. An DDoS attack occurs that day and the highest attack traffic is 45 Gbps. Because 45 Gbps exceeds the base protection bandwidth and triggers the elastic protection, and it falls in the 40 Gbps < elastic bandwidth ≤ 50 Gbps billing range, the elastic cost of that day is charged according to the 40 Gbps < elastic bandwidth ≤ 50 Gbps billing range.

## Need I pay for the attack traffic even after my Anti-DDoS Advanced IP is blocked due to high traffic attack?
The elastic protection billing rules of Anti-DDoS Pro apply to billing of attack traffic that exceeds the base protection bandwidth and is lower than or equal to the elastic protection bandwidth. If the IP is blocked, the attack traffic already exceeds the set elastic protection bandwidth. Therefore, the attack traffic that exceeds the elastic protection bandwidth does not fall in the billing range.

## I purchased the elastic protection service a month ago and no attacks occur. Do I still have to pay?
No elastic protection cost incurs in this case.

## If I have purchased 100 Gbps of base protection bandwidth, can I reduce it to 50 Gbps?
No. The base protection does not support upgrade or degradation.

## Can I raise the elastic protection bandwidth when my business is being attacked?
Yes. On the basic information page of Anti-DDoS Pro, you can upgrade or degrade the elastic protection bandwidth. The elastic protection bandwidth varies depending on the region. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747).
>If fees of the attack traffic are already incurred on the day you modify the bandwidth, you will be charged according to the modified elastic protection bandwidth the next day.

## If a protected IP is attacked several times in a day, will I be charged repeatedly?
The Anti-DDoS Pro service is billed based on the highest attack traffic bandwidth during the day and is only billed for once in a day.

## If I purchase two Anti-DDoS Pro instances, and the attack traffic bandwidths for both of them exceed the base protection bandwidth, how do I pay for the elastic protection?
The elastic protection is billed by instance. If both attack traffic bandwidths of the Anti-DDoS Pro instances exceed the base protection and are within the elastic protection range, you need to pay for the elastic protection of these two instances separately.
