[//]: # (chinagitpath:XXXXX)

## Am I billed in the same method for using the elastic defense service offered with Anti-DDoS Advanced? How am billed?
Yes, you are. You will be billed based on the elastic protection bandwidth corresponding to the protectable attacking traffic during the day. See [Billing Overview](https://cloud.tencent.com/document/product/1014/31100) for more billing details.
For example, you have purchased an Anti-DDoS Advanced instance with 20 Gbps of base protection bandwidth and 50 Gbps of elastic protection bandwidth. If your instance experiences DDoS attacks that generate 45 Gbps of attacking traffic in a day, you are beyond the base protection bandwidth and within the 40 Gbps < elastic protection bandwidth ≤ 50 Gbps range. The elastic defense service used that day is billed based on this range.

## If my IP protected by Anti-DDoS Advanced is blocked after suffering a high-traffic attack, will I be billed for this traffic?
According to the billing rules for the elastic defense service offered with Anti-DDoS Advanced, you will only be billed for attacking traffic that is larger than the base protection bandwidth and less or equal to the elastic protection bandwidth. Your IP being blocked means that the attack traffic has exceeded the elastic protection bandwidth, so you will not be billed for the attacking traffic in excess of that bandwidth.

## If my IP does not experience any attack for a month after my purchase of the elastic defense service, will I be billed?
In this case, you will need to pay the monthly fee for the base defense; no extra charge will apply.

## If I have purchased 100 Gbps of base protection bandwidth, can I reduce it to 50 Gbps?
No. The base protection bandwidth can only be raised, but not reduced.

## Can I raise the elastic protection bandwidth when my application is being attacked?
Yes. You can increase and decrease elastic protection bandwidth on the Anti-DDoS Advanced Basic Info page. The available protection capacity varies from region to region. For details, please see [Product Overview](https://cloud.tencent.com/document/product/1014/31091).
>!If you have been billed for attacks on the day you make the adjustment, you will be billed based on the new elastic protection bandwidth starting the next day.

## If a protected IP suffers more than one attack during a day, will I be billed repeatedly for those attacks?
The Anti-DDoS Advanced service is billed based on the peak attacking traffic during the day and for once only.

## If I have purchased two Anti-DDoS Advanced service packs, and the base protection bandwidth limits of both Anti-DDoS Advanced instances are exceeded, how will I be billed for elastic protection?
The elastic protection service is billed per instance. If you have exceeded the base protection bandwidth for both of the two instances, you will be billed separately for each of them.

