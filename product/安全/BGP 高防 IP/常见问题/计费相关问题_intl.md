[//]: # (chinagitpath:XXXXX)

## Does the same billing model apply to the Anti-DDoS Advanced elastic defense services? How is it calculated?
Yes. You will be billed depends on what range your daily elastic protection bandwidth falls within. See [Billing Overview](https://cloud.tencent.com/document/product/1014/31100) for more billing details.
For example, you have an Anti-DDoS Advanced instance with 20 Gbps base protection bandwidth and 50 Gbps elastic protection bandwidth. If your instance experiences a DDoS attack that generates 45-Gbps traffic flow in a day. The number exceeds the base protection bandwidth limit and thus elastic protection is activated and traffic flow speed falls within a range from 40 Gbps to 50 Gbps.  So instead of paying for the actual usage. 
you will pay for the elastic protection bandwidth based on this range. 

## Should I pay for the attack traffic even after my Anti-DDoS Advanced IP is blocked?
No. According to the billing model mentioned above, and because your IP is automatically blocked when the attack traffic exceeded the elastic protection bandwidth, you only need to pay for the difference between the base protection bandwidth limit and the elastic protection bandwidth limit.  The amount of traffic that exceeds the elastic protection bandwidth limit will not be calculated. 

## What if my IP has not experienced any attacks in a month since I purchased the elastic defense service, how do I pay?
In this case, you will need to pay the monthly fee for the base defense; no extra charge will apply.

## If I have purchased base protection bandwidth with a speed of 100 Gbps, can I reduce the bandwidth speed to 50 Gbps?
No. You can only increase the base protection bandwidth. Unfortunately, the downgrade is not allowed.

## Can I increase the elastic protection bandwidth when my application is being attacked?
Yes. You can increase and decrease elastic protection bandwidth on the Anti-DDoS Advanced Basic Info page. The available options vary by region. For details, please see [Product Overview](https://cloud.tencent.com/document/product/1014/31091).
>!If the charge of attack traffic already has incurred on the day you make the adjustment, you will be billed based on the new plan starting the next day.

## If a protected IP suffers more than one attack during a day, will I be billed repeatedly for those attacks?
The Anti-DDoS Advanced service is billed based on the peak attacking traffic during the day and for once only.

## If I have purchased two Anti-DDoS Advanced instances, and the base protection bandwidth limits of both Anti-DDoS Advanced instances are exceeded, how do I pay for the elastic protection?
You need to pay for the instances separately if both of them have exceeded their base protection bandwidth limits.
