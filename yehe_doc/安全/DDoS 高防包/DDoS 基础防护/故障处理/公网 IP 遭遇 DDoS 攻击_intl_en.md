
## Problem
DDoS attacks overwhelm your business with massive amounts of traffic, exhausting the server performance and network bandwidth and thus crashing down the server.

## Common Cause
Tencent Cloud’s free basic protection capability (2 Gbps) is not enough to defeat the DDoS attacks.

## Solutions
- **Replace a public IP (expedient)**
When attackers start DDoS attacks against your specific business IP, you can avoid the blocking trouble temporarily by replacing the attacked IP with a new one. However, the new IP is still exposed to DDoS attacks, causing potential business interruptions.
- **Get an Anti-DDos product (recommended)**
By getting an Anti-DDoS instance, you can improve IP protection capability to defend against large traffic attacks. If the Anti-DDoS Pro instance of the region is unable to defeat massive attack traffic, you can use an Anti-DDoS Advanced instance with greater protection capability as needed.

## Directions
### Replace a public IP (expedient)
The use limits are as follows:
- Each account can change public IP addresses in the same region a maximum of 3 times per day.
- Each instance can only change its public IP once.
- The old public IP will be released after it is replaced.

For details, see [Changing Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/16642).

### Get and set an Anti-DDoS product (recommended)
- To learn more about purchasing and configuring an Anti-DDoS Pro instance, see [Purchase Directions](https://intl.cloud.tencent.com/document/product/1029/36115) and [Getting Started](https://intl.cloud.tencent.com/document/product/1029/36116).
- To learn more about purchasing and configuring an Anti-DDoS Advanced instance, see [Purchase Directions](https://intl.cloud.tencent.com/document/product/297/37241) and [Getting Started](https://intl.cloud.tencent.com/document/product/297/37202).

For details on differences between Anti-DDoS Pro and Anti-DDoS Advanced instances, see [Comparison of Anti-DDoS Protection Schemes](https://intl.cloud.tencent.com/document/product/1029/36110).

