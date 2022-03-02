
## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of Internet traffic.
### Network layer DDoS attack
A network layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhausting its system layer resources with a flood of Internet traffic.
Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks.
### CC attack
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application layer resources and exhausting its processing capacity.
Common attacks include HTTP/HTTPS-based GET/POST Flood, layer-4 CC, and connection flood attacks, etc.

## [Protection Bandwidth](id:fhfz)
There are two types of protection bandwidth: base protection bandwidth and elastic protection bandwidth.
- Base protection bandwidth: base protection bandwidth of the Anti-DDoS Advanced instance, which is on the monthly-subscribed frozen fees payment.
- Elastic protection bandwidth: the largest possible protection bandwidth of the Anti-DDoS Advanced instance. The part that exceeds the base protection bandwidth is billed on a daily pay-as-you-go basis.

If elastic protection is not enabled, the maximum bandwidth of an Anti-DDoS Advanced instance will be the base protection bandwidth. If elastic protection is enabled, the maximum bandwidth will be the elastic protection bandwidth. Once the attack traffic exceeds the maximum protection bandwidth, IP blocking will be triggered.
>? Elastic protection is disabled by default. If you need the feature, please check the pricing and billing information and enable it yourself. You can adjust the elastic protection bandwidth as required.

### Benefits of elastic protection bandwidth
With elastic protection enabled, when the attack traffic is higher than the base protection bandwidth but lower than the elastic protection bandwidth, Tencent Cloud Anti-DDoS Advanced will continue to protect your IPs to ensure the continuity of your application.

### Elastic protection billing
With elastic protection enabled, elastic protection will be triggered and incur fees once the attack traffic goes over the base protection bandwidth. You will be billed on the following day based on the peak attack bandwidth of the current day.
For example, assume that you have purchased 20 Gbps of base protection bandwidth and set the elastic protection bandwidth as 50 Gbps. If the actual peak attack bandwidth of the day is 35 Gbps, you will need to pay for the elastic protection according to the price of the 30-40 Gbps tier.

