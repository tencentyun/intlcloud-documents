TTL (time to live) is the period of time during which the DNS servers in various regions cache the resolution records.

Assuming that the TTL is set to 10 minutes, when a DNS server receives a domain name resolution request, it will send a request to the authoritative server to obtain the resolution record and save it for 10 minutes on the local server. The record will be read from the local cache for resolution requests within the 10 minutes and the record value will be reacquired after the cache expires. It is recommended to set it at 10 minutes under normal conditions. The minimum TTL values that can be set vary for different resolution package editions.

| Resolution package edition | Minimum TTL |
|---|---|
| Free edition | 600s |
| Personal Professional edition | 120s |
| Enterprise Basic edition | 60s |
| Enterprise Standard edition | 1s |
| Enterprise Ultimate edition | 1s |
