### Does Tencent Cloud DNSPod support pan resolution for third-level domain names?
Yes.

### Does Tencent Cloud DNSPod provide domain name registration or hosting services?
No. Currently, Tencent Cloud DNSPod only provides domain name resolution services.

### How does Tencent Cloud DNSPod tell different search engines from one another?
Tencent Cloud DNSPod has an library of search engine spider IPs, with a separate 360 search engine line in the Enterprise III package.

### Does Tencent Cloud DNSPod support domain name 301 redirect?
Yes. DNSPod's explicit URL is 301 redirect.

### Can I make a website inaccessible to specified regions?
Yes. The province-specific resolution function in the package can do this. For details, please contact our sales team. 

### What are the common ways of DNS hijacking? How should webmasters and netizens respond?
There are two service roles in DNS: recursive DNS and authoritative DNS. Authoritative DNS controls website resolution, while recursive DNS only acts as a cache. Therefore, what matters to webmasters is authoritative DNS, i.e., the DNS address entered in the domain name registrar, while the netizens use recursive DNS.  
**There are two types of DNS hijacking:**  
1. Hijacking of authoritative DNS  
There are two forms of this kind of attacks. The first is to control the account at the domain name registrar. For example, a few years ago, a hacker attacked a company's account at the domain name registrar and modified the NS record of xx.com, which was like changing the authoritative DNS. That was control of the content at the source, so all recursive DNS servers were contaminated and all netizens were redirected to the wrong page. At that point, if we checked with tools such as dig or nslookup, we would have found that all the content of the DNS server was incorrect. To resolve that issue, we need to not only change the NS record back to our own authoritative DNS server, but also wait for all recursive DNS servers' caches to expire and the data to be refreshed before we can access the correct website. The second is to invade the authoritative server to fully control it, which is more difficult to do.  
2. Hijacking of recursive DNS    
If the DNS uses unreliable UDP packets for communication, an attacker may have the opportunity to impersonate an authoritative DNS server and use fake data to deceive the recursive DNS. Attacks against the recursive DNS are usually regional. For example, if a hacker attacks one or several recursive DNS servers, only access using those servers is affected. In this case, using dig or nslookup to test will reveal that some recursive DNS servers are incorrect but some work properly.  

For ordinary netizens, it is recommended to use a more secure recursive DNS server, such as 8.8.8.8 of Google. Usually, we believe that Google's DNS is less likely to be hijacked because of Google's technical strength, so if the result returned by 8.8.8.8 is correct, then the authoritative DNS service is normal. For most webmasters, it is recommended to keep the account registered at the domain registrar secure and use an authoritative DNS service provider with strong technical expertise.
