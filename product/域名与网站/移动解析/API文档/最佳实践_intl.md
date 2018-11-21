In the process of accessing HttpDNS, the domain name resolution mechanism of the mobile app needs to be modified. The new process is as follows:

![HttpDNS best practice](https://main.qcloudimg.com/raw/2425510c2248fcb6aa84c3b6fa3fe620.png)

The following two design strategies need to be followed during the transformation process:

### 1. Failover Strategy
Although HttpDNS has been connected to BGP Anycast and achieved cross-region cross-IDC disaster recovery, in order to ensure that the client domain name resolution is unaffected in the worst case, the following failover strategy is recommended:
- The first step is to initiate a domain name query request to HttpDNS.
- If the result returned by the HttpDNS query is not an IP address (the result is empty, the result is not an IP or the connection timed out), domain name resolution is performed through the LocalDNS. The timeout is recommended to be 5 seconds.

### 2. Cache Strategy
The network environments of mobile Internet users are very complicated. In order to minimize the delay caused by domain name resolution, creating a local cache is recommended. The caching rules are as follows:
- Cache time
The cache time is recommended to be set at 120 to 600 seconds and cannot be less than 60 seconds.

- Cache update
Cache updates should be done in the following two situations:
**When the end user's network status changes:**
If the network connection of the mobile Internet user is switched between 3G and Wi-Fi, the ISP of the access point may change. Therefore, when the network status of the user changes, the domain name resolution request needs to be re-initiated to HttpDNS to obtain the optimal direction under the user's ISP.
**When the cache expires:**
When the cache of domain name resolution result expires, the client need to re-initiate a domain name resolution request to HttpDNS to obtain the latest IP corresponding to the domain name. To reduce the waiting time of re-doing domain name resolution after the cache expires, it is recommended to start domain name resolution at 75% TTL. If the TTL of the local cache is 600 seconds, then at second 600 x 0.75 = 450, the client should perform domain name resolution.

In addition to the suggestions above, reducing the number of domain name resolutions can also effectively reduce network interaction and improve user access experience. It is recommended to minimize the number of domain names as the business allows. If you want to distinguish among different resources, it is recommended to differentiate them by the URL.

### 3. Other Precautions

Tips for transforming the app:

1. Try to use the same domain name for different functions. The resources can be differentiated by the URL. Reduce the number of domain name resolutions for a better user experience and easier switching for disaster recovery. One more domain name, even with a hit in the cache, at least increases 100 ms of access delay. A new version will soon support bulk domain name resolution.
2. Do not set a too low value for the cache TTL (no less than 60 seconds). This helps prevent frequent HttpDNS requests.
3. The business that accesses HttpDNS needs to retain the LocalDNS of the user as the disaster recovery channel, so when HttpDNS cannot serve normally (due to unstable mobile network or HttpDNS service failure), the LocalDNS can be used for resolution.
4. If a 404 error occurs in an Android app but it is normal in the browser, this may be due to a permission issue or other issues. For more information, see http://stackoverflow.com/questions/10835845/android-http-request-wierd-404-not-found-issue.
5. For bytetohex & hextobyte, you need to implement the API on your own to perform hexadecimal string and byte conversion.
6. For HTTPS issues, you need to check the domain and extension field of the certificate in the client hook to see if it contains the host process of the request, and then directly replace the IP with the original domain name to retry certificate verification. Or, ignore certificate verification (similar to the curl -k parameter).
7. The HttpDNS request timeout is recommended to be around 2 to 5 seconds.
8. When the network type changes between 4G and Wi-Fi or between two different Wi-Fi networks, re-execute the HttpDNS request to refresh the local cache.
