## Client Connection Process
When connecting to HTTPDNS, you need to modify the DNS mechanism on the mobile client as instructed below:

![](https://main.qcloudimg.com/raw/14701588dd29f0af9e0a793753e99b32.jpg)



Client; Query the local cache; Is there cache locally?; Does the local cache reach 75% of the TTL?; Return the query result; Send a DNS query to HTTPDNS; Is the result returned by HTTPDNS an IP?; Update the local cache; Send a DNS query to the local DNS

## Design Policy
Follow the following two design policies during modification:

### Failover policy
Although HTTPDNS has been connected to BGP Anycast and implemented multi-region cross-IDC disaster recovery, to ensure that the DNS on the client will not be affected even in the worst case, we recommend you use the following failover policy:
1. Send a DNS query to HTTPDNS.
2. If the result returned in response to an HTTPDNS query is not an IP address (empty, non-IP, or connection timeout), the DNS query will be performed by the local DNS. We recommend you set the timeout period to 5 seconds.

### Cache policy
As the network environments of mobile internet users are complex, to minimize the delay caused by DNS query, we recommend you perform local caching. The caching rules are as follows:
- **Cache validity**: We recommend you set the cache validity to 120s–600s. It should not be below 60s.
- **Cache update**:
The cache should be updated in the following two scenarios:
 - **When the user's network status changes:**
When a mobile internet user switches from 3G to Wi-Fi or from Wi-Fi to 3G, the network of their access point may change. At this point, you need to send a DNS request to HTTPDNS again to get the optimal direction for the user's current network.
 - **When the cache expires:**
When the cache of the DNS query result expires, the client should send a new DNS request to HTTPDNS to get the IP associated with the latest domain. To shorten the wait before a new DNS query is performed, we recommend that the DNS query be performed at 75% of the TTL. For example, if the TTL of the local cache is 600s, the client should perform a DNS query at the 600 \* 0.75 = 450th second.

In addition to the above suggestions, reducing the number of DNS queries can also effectively reduce network interactions and improve the user access experience. We recommend you minimize the number of domains as long as your business permits. To distinguish between different resources, we recommend you use URLs.

## Notes
In order for you to better modify the mobile client, read the following notes first:
- Implement different features with the same domain but different URLs so as to reduce the number of DNS queries. This delivers a better user experience and makes failover easier. This is because each additional domain, even if it has a hit in the cache, will result in an increase of at least 100 milliseconds in the access delay.
- The TTL value of the cache should not be too low (at least above 60s) so as to avoid sending frequent requests to HTTPDNS.
- The business connected to HTTPDNS needs to retain the user's local DNS as a backup, so that when HTTPDNS cannot work properly (due to an unstable mobile network or HTTPDNS problem), the local DNS can be used.
- A 404 error may occur in Android applications, but if the browser access is normal, it may be a permission problem. For more information, see [Android HTTP request 404 not found issue](https://stackoverflow.com/questions/10835845/android-http-request-wierd-404-not-found-issue).
- For `bytetohex` and `hextobyte`, you need to implement the APIs on your own to convert between hexadecimal strings and bytes.
- For HTTPS problems, you need to hook the client to check whether the domain and domain extension of the certificate contain the host in the request and replace the IP with the original domain before performing a certificate verification again. You can also ignore certificate verification (similar to the `-k` parameter in curl).
- We recommend you set the timeout period for HTTPDNS requests to 2–5s.
- When the network type changes, for example, from 4G to Wi-Fi or from one Wi-Fi network to another, you need to execute HTTPDNS requests again to purge the local cache.



