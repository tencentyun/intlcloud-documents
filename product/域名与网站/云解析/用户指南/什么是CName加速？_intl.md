### Features
CNAME acceleration is a Tencent Cloud DNSPod's proprietary feature designed to solve the issue where the resolution time is increased due to the fact that the recursive server needs to request the authoritative server multiple times if the user sets a multi-hop CNAME resolution record.
Suppose that a.com, b.com and c.com are all domain names resolved by DNSPod:
A CNAME record is set for `www.a.com`, with a record value of `www.b.com`
A CNAME record is set for `www.b.com`, with a record value of `www.c.com`
An A record is set for `www.c.com`, with a record value of 1.2.3.4
In general, the recursive server is required to send three requests to the authoritative server to get the IP address of `www.a.com` as shown in the figure below:
![Acceleration-1](https://mc.qcloudimg.com/static/img/57938b0d24aa1a136c852c0cf0d1abc3/123.png)
After CNAME acceleration is enabled, the authoritative server returns the CNAME record and the final A record together to the recursive server at a time, so the recursive server only needs to make one instead of three requests as shown in the figure below:
![Acceleration-2](https://mc.qcloudimg.com/static/img/a8b35c14692209372897e985990be3a6/123.png)
This greatly reduces the time spent on network communication in requests and responses, making resolution faster, especially when a multi-hop CNAME resolution record is configured.
### Acceleration Effect
Before CNAME acceleration is enabled: query-time 1021 msec:
![1](https://mc.qcloudimg.com/static/img/a3b44b2e056e921ca1adac9e5dfb77d3/speedup_off.png)
After CNAME acceleration is enabled: query-time 410 msec:
![2](https://mc.qcloudimg.com/static/img/f71dfc679621faff5a93889f56c9ac48/speedup_on.jpg)
The resolution time is reduced by 59.84% with significant acceleration effect.
>**Note:**
>This test is conducted after clearing the cache and setting TTL as expired.

### Precautions
1. The domain name for which to enable CNAME acceleration must use Tencent Cloud DNS or DNSPod services; otherwise, the feature cannot be enabled or the acceleration fails. In severe cases, resolution errors may be caused;
2. For a domain name that has CNAME acceleration enabled, if the system detects that it doesn't use Tencent Cloud DNS services (for example, the domain name registration expires or the domain name is moved to another DNS provider), CNAME acceleration will be automatically disabled, and after the system detects that the domain name resumes using Tencent Cloud DNS or DNSPod services, CNAME acceleration will be automatically enabled again;
3. CNAME acceleration doesn't need to be enabled for different subdomain names under the same domain name as the system will automatically accelerate resolution for them;
4. CNAME acceleration should be disabled before the domain name is transferred. If the domain name has already been transferred but the system hasn't scanned its current status yet, you can disable CNAME acceleration or contact the technical support to do so.
