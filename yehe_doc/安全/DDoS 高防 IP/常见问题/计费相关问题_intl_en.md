### What should I do if I want to end the Anti-DDoS Advanced service?

Anti-DDoS Advanced adopts a pay-as-you-go model. If you want to end the service, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to terminate your instances. Otherwise, charges are still be incurred.

- After you apply for a termination in the current month, the monthly-subscribed items will be settled as usual, while the daily billable items are settled based on the actual usage. After you terminate your instances, the service will be stopped immediately and the instances will no longer be billed for the next month.
- The entire termination takes 1-3 working days to complete and is subject to the actual operation (protection fees may be incurred during the period).

### Are the billing modes the same for elastic protection of different Anti-DDoS services? How are the fees for elastic protection calculated?
Yes, they are. Elastic protection is billed based on the tiered price of the peak attack traffic bandwidth of the day. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/297/17435).
For example, you have purchased an Anti-DDoS Advanced instance with 20 Gbps base protection bandwidth and 50 Gbps elastic protection bandwidth. A DDoS attack occurs one day with the peak attack traffic bandwidth of 45 Gbps. Since 45 Gbps exceeds the base protection bandwidth and triggers elastic protection, and it falls between 40 Gbps and 50 Gbps, the fees for elastic protection of the day will be billed according to the tiered price of the billing tier between 40 Gbps and 50 Gbps.

### If the IP protected by my Anti-DDoS Advanced instance is blocked due to high traffic attacks, will I be billed for the attack traffic over the maximum protection bandwidth?
No. You will be billed for elastic protection when the attack traffic exceeds the base protection bandwidth but lower than or equal to the elastic protection bandwidth. If your IP is blocked, it means that the attack traffic already exceeds the elastic protection bandwidth. Therefore, you will not be billed for the excessive attack traffic.

### I enabled elastic protection a month ago, but no attack has occurred so far. Do I still have to pay for the feature?
In this case, you only need to pay the monthly subscription fees for base protection. No additional fees will be incurred.

### Can I increase the elastic protection bandwidth when my business is under attack?
Yes. You can increase or reduce the elastic protection bandwidth of Anti-DDoS Advanced. The protection capability varies by region. For more information on the range of elastic protection bandwidth, please visit the purchase page.
>If protection fees have already been incurred on the day you make the modification, you will be billed according to the latest elastic protection bandwidth on the following day.

### If a protected IP is attacked several times in a day, will I be charged repeatedly?
The Anti-DDoS Advanced service is billed based on the peak attack traffic bandwidth during a day. Therefore, you will not be charged repeatedly for multiple attacks during a day.

### I purchased two Anti-DDoS instances, and both of them are under attack traffic that exceeds the basic protection bandwidth. How will I be charged for elastic protection?
Elastic protection is billed by instance. If both of your Anti-DDoS instances are under attack traffic that exceeds the basic protection bandwidth, you will need to pay for elastic protection for the two instances separately.
