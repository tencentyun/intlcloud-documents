[//]: # (chinagitpath:XXXXX)

## Scenarios
On-line running applications have their specific settings and restrictions. The interruption of these applications may cause severe consequences. Before integrating your applications to Anti-DDoS Advance, please follow the suggestions below to reduce possible risks.

## Suggestions
>! Please note that Tencent Cloud provides the following suggestions replying on its own experience earned from other customer cases. You should improve and supplement the solution according to your actual situation.

### Technical Suggestions
1.	Modify the local hosts file instead of modifying the DNS A record directly. The QA team should conduct a local test to check the availability, latency, etc..
2.	If an intelligent domain name resolution product is used, you can change the A record for specified ISPs or regions, redirecting some of the traffic to Anti-DDoS IP for beta test first, and complete the rest gradually.
3.	Shorten the TTL of a DNS record for faster disaster recover.
4.	Prepare a rollback plan in case of any problem

### Priority
1. Migrate backed up, non-important, and non-critical applications first.
2. Implement migration during non-busy period.

