## IPv6-related FAQs
### Does Tencent Cloud DNS support IPv6-only environments?  
Tencent Cloud DNSPod supports IPv6-only network environments with verified performance outside mainland China.
### An iOS app passes the local testing but is rejected when submitted to the App Store. Why?  
* **Check whether the issue is caused by DNS resolution failure**  
How can you verify that the DNS server responds correctly to the resolution request to an IPv6 address? After setting up the DNS64 environment, you can query it by executing the following command:
```
$ dig dnspod.cn aaaa
```
The reason for verifying DNS resolution is that the first step for the app to access the Internet is to perform DNS resolution. When the App Store reviews the iOS app, it will first access the DNS server, obtain the IPv6 address of the app server, and then access it. If the DNS server cannot resolve successfully to the IPv6 address, even if the app passes the testing in a locally built IPv6-only environment, it will still be rejected by the App Store. Therefore, it is vital to choose a domain name resolution service that has both high stability and compatibility.
* **Poor cross-border network connection quality**  
DNS generally completes GEO region-specific resolution through an IP address library, but IPv6 does not have such an address library, so all IPv6 resolutions are resolved to the address of the default line. If the default line is set to a China Telecom or BGP IP (for CAP, the default is China Telecom), it will be much likely that the connection from an overseas location will fail due to the poor cross-border connection quality of China Telecom, leading to rejection by the App Store. It is recommended to:    
 1. Modify the default IP of the domain name for the functions required during the review to a China Unicom or China Mobile IP.
 2. Connect the functions required during the review to Dynamic Site Accelerator to speed up cross-border access.

### How do I make an iOS app support IPv6-only environments?  
Currently, there are three ways to enable an iOS app to support IPv6-only environments, as detailed below:    
* Connect all domain names in the app to DNSPod  
Both Tencent Cloud's underlying DNS resolution and DNSPod's DNS support IPv6-only environments, ensuring that businesses are successfully resolved in IPv6-only environments. The iOS app server does not need to support IPv6, as in IPv6-only environments, DNS64/NAT64 can translate IPv4 addresses into IPv6 addresses.
* Transform the client  
For example, you can transform the client to fix issues with direct IP access or upgrade the SDK APIs to make them compatible with IPv6.
* Set up and verify the environment  
See [Apple's official documentation](https://developer.apple.com/library/ios/documentation/NetworkingInternetWeb/Conceptual/NetworkingOverview/UnderstandingandPreparingfortheIPv6Transition/UnderstandingandPreparingfortheIPv6Transition.html#//apple_ref/doc/uid/TP40010220-CH213-SW1) to create an IPv6-only hotspot and connect to it using an iPhone for testing.

## Other IP-related FAQs
### Can Tencent Cloud DNSPod hide IP resolution?
DNS cannot hide the IP as it maps domain name to IP.  
### Both a China Telecom IP and a China Unicom IP have been specified for a domain name, but sometimes one of them doesn't work. Can I set automatic pause for the malfunctioning one?
This can be done using the D Monitor.
For details, see [D Monitor User Guide](https://support.dnspod.cn/Kb/showarticle/?qtype=%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%BB%8D%E5%8F%8A%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B&tsid=16).
### After a record is deleted/paused, why can I still ping the IP?
This is caused by the cache of the local ISP's server (recursive server). Please wait patiently for the local cache to invalidate. Theoretically, the cache will become invalid after the TTL time set for the record lapses.
### Why are the resolution result of the domain name and the resolved IP different?
It is recommended to use the **Quick Diagnostics** tool in DNSPod's **Help Center** for diagnosis. If you changed the DNS service provides less than 72 hours ago and changed the server address, please wait patiently for the change to take effect.  
### In intelligent resolution, why is a China Unicom user resolved to the IP of a China Telecom server?
1. First, confirm that the network you are using is not a line of Hangzhou Wasu or Beijing Great Wall Broadband Network.
2. The resolution using DNSPod was configured less than 72 hours ago. Please wait patiently for the resolution to take effect.
3. The China Unicom server is down, so D Monitor automatically switches the record value of the China Unicom line to the IP of the China Telecom server. After the China Unicom server is back online, the record value will be automatically switched back to its IP. 
4. You can visit `http://ip.dnspod.cn` in a browser to check whether the local DNS matches the line. If not, modify the local DNS.
5. Check whether the local servers is set to pointing to an specified IP.

### After the IP is changed for a domain name, why do search engine spiders still crawl the old server?
Different search engines have different update periods (at least one week). After the IP is modified for the domain name, search engines need a period of time to update. Please wait patiently.


