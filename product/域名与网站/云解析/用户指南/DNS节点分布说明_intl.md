Tencent Cloud DNSPod is a world-leading domain name resolution platform with 65 cloud cluster nodes in China and 12 ones overseas. A single DNSPod server can resolve up to 10 million times per second. Currently, DNSPod provides domain name resolution for over 6.5 million domain names with more than 21 billion DNS requests processed per day and more than 2,000 DNS attacks prevented per month.

Multiple nodes in the cluster not only provide local access for end users' resolution requests, but also allow for a comprehensive remote disaster recovery mechanism. In addition, intra-cluster resolution can achieve synchronization at the second level. Records modified on the web can be instantly synced to all backend DNS clusters (between 1 to 5 seconds), making the changes take effect at DNSPod in just seconds (recursive DNS is subject to TTL, so the actual time for the changes to become effective for end users depends on the TTL set in the domain name's resolution record).

The clusters for resolution vary for different package editions, and the corresponding DNS addresses of each cluster are different:

| Resolution package edition | DNS address | Note |
|---|---|---|
| Free DNS address | f1g1ns1.dnspod.net/f1g1ns2.dnspod.net | 10 nodes |
| Personal Professional edition | ns3.dnsv2.com/ns4.dnsv2.com | 12 nodes |
| Enterprise Basic edition | ns3.dnsv3.com/ns4.dnsv3.com | 14 nodes |
| Enterprise Standard edition | ns3.dnsv4.com/ns4.dnsv4.com | 18 nodes |
| Enterprise Ultimate edition | ns3.dnsv5.com/ns4.dnsv5.com | 22 nodes |
