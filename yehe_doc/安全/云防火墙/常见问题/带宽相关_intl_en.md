
### What is bandwidth? How can I select appropriate bandwidth configuration?
- CFW bandwidth is independent from bandwidth of other network products. Therefore, you need to purchase CFW bandwidth separately.
- NAT and CFW are independent from but connected with each other. Therefore, you need to ensure that the CFW bandwidth purchased is the same as or higher than that of NAT, so that both systems meet users' needs for bandwidth or throughput.


### What is peak bandwidth? Does it refer to uplink or downlink bandwidth?
Peak bandwidth refers to the maximum bandwidth in both uplink and downlink directions. For example, if you purchase bandwidth of 100 Mbps, CFW can process traffic of 100 Mbps in both uplink and downlink directions at the same time.

### Does it affect my business when the peak bandwidth is exceeded? [](id:question4)
- The edge firewall is deployed in a bypass mode, so exceeding the peak bandwidth **will not cause a packet loss or affect the traffic speed of your service**; NAT firewall is deployed in a serial mode, so exceeding the peak bandwidth will cause a packet loss. If the public network traffic is higher than the purchased CFW bandwidth, CFW **does not promise to protect the traffic beyond peak bandwidth**. Such traffic will be directly allowed to pass.
- Please keep your eye on CFW bandwidth alerts. In case of high bandwidth, disable the firewall toggle for some networks or expand the bandwidth to ensure normal service running.

### Will the CFW edge firewall bandwidth limit the traffic?
No. CFW does not limit the traffic.

### How is inbound/outbound bandwidth calculated? Will rule matching of inbound traffic be affected when the outbound bandwidth exceeds the purchased configuration?
- Inbound bandwidth and outbound bandwidth are calculated respectively.
- CFW does not promise to protect the traffic beyond the purchased bandwidth configuration. If only the outbound traffic exceeds the upper limit, rule matching of inbound traffic will not be affected.

### Is the bandwidth of edge firewall and NAT edge firewall calculated respectively?
Yes. The bandwidth for them is calculated respectively.
>? The bandwidth of NAT edge firewall is the same as that of edge firewall. You can expand the bandwidth of NAT edge firewall by expanding that of edge firewall.


### Can I scale up or down the CFW bandwidth?
Bandwidth can only be scaled up.

### Does the CFW bandwidth limit depends on the bandwidth of accessed CVM?
No. The CFW bandwidth limit is configured based on actually used bandwidth to ensure that traffic bandwidth consumed at a time does not exceed the bandwidth configuration of CFW.
