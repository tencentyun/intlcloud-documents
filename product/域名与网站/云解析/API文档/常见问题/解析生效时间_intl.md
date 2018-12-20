### What factors influence the time required for a domain name resolution to take effect?
For a domain name registered with Tencent Cloud to be effective, it must take effect at Tencent Cloud DNS first and then at local DNS servers around the world (it is like the resolution record of Tencent Cloud DNS needs to be synced to DNS servers of major ISPs). As the resolution takes effect at Tencent Cloud DNS in real time and then gets synced to local DNS servers in different regions in just seconds, whether the website can be visited depends directly on the local DNS servers. However, since all local DNS servers have a caching mechanism, the actual time for the resolution to take effect relies on the refresh time of those ISPs.
### How long does it take for a new resolution record to take effect?
A new resolution record added in Tencent Cloud DNS takes effect in real time.
### How long does it take for a modified resolution record to take effect?
After modified, a domain name record theoretically will be effective after the TTL previously set for it elapses. However, a local ISP may have forcibly extend the validity of the original record, and in this case, the modified record may not take effect as expected.
### How long does it take for a modified DNS to take effect?
After a domain name is modified by pointing it to DNSPod, although the new resolution takes effect on the DNSPod side in real time, it generally takes 0-72 hours for the resolution to be effective globally due to the fact that ISPs in different regions may have different DNS refresh time. Please wait patiently.  
### After my domain name registered with Tencent Cloud expired, I renewed it successfully without modifying the DNS, but why didn't the resolution work?
The DNS will expire upon expiry of the domain name. After successful renewal, it takes 0-72 hours for the DNS to take effect again. Please wait patiently.
### What should I do if the resolution does not work?
Generally speaking, an ineffective resolution may be in the following two forms:
1. **Page cannot be opened**
As long as there is an error code returned on the page, the resolution has taken effect, and all you need to do is check the server configuration.
The following are common error codes:  
(1) Website under construction
(2) Object not found
(3) Error 404
(4) Access forbidden
(5) Error 403
(6) Forbidden
If any error code listed above appears on the page, it can be said that the error is basically irrelevant to the resolution. Please check the server configuration.
2. **The domain name cannot be pinged. This may be due to the following reasons:**
 1. The record has been incorrectly added
If the default line type is not selected, some users may not be able to access the domain name. **Default line** must be added; otherwise, only the specified lines can access your website. If it is to resolve for two lines, it is recommended to select a **China Telecom IP** for the **Default** line (but you can select a China Unicom or China Mobile IP too if needed).
 2. DNS modification has not taken effect yet
It takes a period of time before the modified DNS takes full effect, so it won't be fully effective in just a few hours. If your local ISP's DNS server has not completely refreshed your domain name record, the IP cannot be pinged. The solution is to keep waiting (usually up to 48 hours).
 3. The DNS record of the domain name has been cached
The cache may be on the Windows operating system (Windows always keeps a cache), the router (if connected to the Internet via routing) or the local ISP's DNS server (which is recursive).

**Solution:**
1. If it is a dial-up Internet connection on Windows, go to **Start** > **Run** > **ipconfig /flushdns** and then wait for around 30 seconds before pinging again. The issue generally can be fixed.
 ![1](https://mc.qcloudimg.com/static/img/5df3391c4144c0cb0963481cee4f93f9/1.png)
2. If it is an Internet connection via a router, the DNS cache of the router needs to be cleared. This can be done by rebooting the router, and if the router cannot be rebooted, the DNS server of Windows has to be replaced with another address.
>**Note:**
>To clear the router cache by this method, you also need to run the ipconfig /flushdns command. 

3. If none of the methods above works, the problem would definitely be that the local ISP's DNS server has cached the record data. In this case, you can replace the DNS server of Windows with another address or wait the local ISP's DNS server to clear the cache (usually within an hour).
>**Note:**
>Linux and Unix do not cache DNS records. On Mac OS X, you can use the killall lookupd command to clear the DNS cache.
