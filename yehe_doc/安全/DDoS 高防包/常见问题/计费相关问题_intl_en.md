### What should I do if I want to end the Anti-DDoS Pro service?

Anti-DDoS Pro adopts a pay-as-you-go model. If you want to end the service, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to terminate your instances. Otherwise, charges are still be incurred.

- After you apply for a termination in the current month, the monthly-subscribed items will be settled as usual, while the daily billable items are settled based on the actual usage. After you terminate your instances, the service will be stopped immediately and the instances will no longer be billed for the next month.
- The entire termination takes 1-3 working days to complete and is subject to the actual operation (protection fees may be incurred during the period).


### If a protected IP is attacked several times in a day, how will be the consumption of protected times calculated?
Max protection of Anti-DDoS Pro: when the attack traffic to a protected IP in the instance is detected to be at least 10 Gbps and there is no attack traffic after half an hour, the attack will be considered to be over, and one max protection will be deducted; if the attack continues for more than half an hour, one max protection will not be deducted until the attack is over.

### What are the differences between the max protection billing of Anti-DDoS Pro and elastic protection billing of Anti-DDoS Advanced?
When an attack occurs, the maximum DDoS protection capability of Tencent Cloud in the region of the Anti-DDoS Pro instance will be automatically called to provide max protection, which is included in the instance and will not incur additional elastic protection fees.
The elastic protection of Anti-DDoS Advanced is billed by the bandwidth of the elastic protection range corresponding to the maximum attack traffic generated on the day.

