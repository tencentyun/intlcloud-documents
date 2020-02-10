## Are the billing modes the same for elastic protection of different Anti-DDoS services? How are the fees for elastic protection calculated?
Yes, they are. Elastic protection is billed based on the tiered price of the peak attack bandwidth of the day. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747).
For example, you have purchased an Anti-DDoS Pro instance with 20 Gbps base protection bandwidth and 50 Gbps elastic protection bandwidth. An DDoS attack occurs one day with the peak attack bandwidth of 45 Gbps. Since 45 Gbps goes over the base protection bandwidth and triggers elastic protection, and it falls between 40 Gbps and 50 Gbps, the fees for elastic protection of that day will be billed according to the tiered price of the billing tier between 40 Gbps and 50 Gbps.

## If the IP protected by my Anti-DDoS Pro instance is blocked due to large traffic attacks, will I be billed for the attack traffic over the maximum protection bandwidth?
You will be billed for elastic protection when the attack traffic is over the base protection bandwidth but lower than or equal to the elastic protection bandwidth. If your IP is blocked, it means that the attack traffic already exceeds the elastic protection bandwidth. Therefore, you will not be billed for the attack traffic that exceeds the elastic protection bandwidth.

## I enabled elastic protection a month ago but no attack has occurred so far. Do I still have to pay for the feature?
You will not be billed for elastic protection in this case.

## I purchased 100 Gbps of base protection bandwidth. Can I downgrade it to 50 Gbps?
No. You can upgrade but not downgrade your base protection bandwidth.

## Can I raise the elastic protection bandwidth when my business is under attack?
Yes. On the basic information page of your Anti-DDoS Pro instance, you can upgrade or degrade the elastic protection bandwidth. The elastic protection bandwidth varies depending on the region. For the billing tiers of the elastic protection bandwidth, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747).
>If protection fees have already been incurred on the day you modify the bandwidth, on the following day you will be billed according to the latest elastic protection bandwidth.

## If a protected IP is attacked several times in a day, will I be charged repeatedly?
The Anti-DDoS Pro service is billed based on the peak attack bandwidth during a day. Therefore, you will not be charged repeatedly for multiple attacks during a day.

## I purchased two Anti-DDoS Pro instances, and both of them are under attack traffic that exceeds the basic protection bandwidth. How will I be charged for elastic protection?
Elastic protection is billed by instance. If both of your Anti-DDoS instances are under attack traffic that is over the basic protection bandwidth but within the elastic protection bandwidth, you will need to pay for the elastic protection of the two instances separately.
