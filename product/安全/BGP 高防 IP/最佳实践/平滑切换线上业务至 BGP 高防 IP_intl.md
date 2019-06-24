## Why appropriate switching is necessary
There could be many special configurations and restrictions for currently running online applications, and service downtime may have negative impact on business. Therefore, we recommend that you follow the suggestions below to adopt appropriate switching mode and avoid possible risks before integrating Anti-DDoS Advanced to your currently running applications.

## Suggestions
> Please note that the following suggestions are based on what we have learned from serving other Tencent Cloud customers. We recommend you adjust or improve the solution according to your actual situation to minimize risks.

### Technical Suggestions
1.    Modify local hosts file instead of DNS A records. The QA team should test and measure relevant performance indicators such as availability and latency.
2.    With an intelligent DNS product, you can change the A record for specified ISPs or regions, redirect a little amount of traffic to Anti-DDoS IP for beta before fully applying Anti-DDoS Advanced to your business applications.  
3.    Shorten the TTL of a DNS record for faster disaster recovery.
4.    Prepare roll-back strategies in advance, and back off as soon as the problem arises.

### Priority
1. Migrate Backup applications and non-critical business applications first.
2. Migrate the applications during off-peak hours.

