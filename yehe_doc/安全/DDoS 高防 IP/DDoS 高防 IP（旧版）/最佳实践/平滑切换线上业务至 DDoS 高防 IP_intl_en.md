## Background
There could be many special configurations and restrictions for currently running online applications, and service downtime may have negative impact on business. Therefore, you are recommended to follow the suggestions below to adopt appropriate switching mode and avoid possible risks before integrating Anti-DDoS Advanced to your online applications.

## Suggestions
>Please note that the following suggestions are based on what we have learned from serving other Tencent Cloud customers. You are recommended to adjust or improve the scheme according to your actual situation to minimize risks.

### Technical suggestions
- Modify local hosts file instead of the DNS A record. The testing team should locally test and measure relevant performance metrics such as availability and latency.
- With an intelligent DNS product, you can change the A record for specified ISPs or regions, redirect a little amount of traffic to Anti-DDoS Advanced IP for test before fully applying Anti-DDoS Advanced to your business applications.
- Shorten the TTL of the DNS record for faster disaster recovery.
- Prepare a rollback plan in advance and back off as soon as any problem arises.

### Priority
- Migrate standby and non-critical business applications first.
- Migrate the applications during off-hours.
