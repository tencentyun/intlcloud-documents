### What are the uses of the "host" field?
The "host" field refers to the domain name prefix with the following common uses:
**www:** The resolved domain name is `www.87677677.com`
**@:** It directly resolves the primary domain name as `87677677.com`
***:** It is pan resolution and matches all other domain names `*.87677677.com`

### What is the meaning of record type?
To point to an IP address provided by a host service provider, select A for the type; to point to a domain name, select CNAME for the type.
**A record:** Address record used to specify the IPv4 address (e.g., 8.8.8.8) of a domain name. If you need to point a domain name to an IP address, you need to add an A record.
**CNAME record:** If you need to point a domain name to another one which will be used to provide the IP address, you need to add a CNAME record.
**NS record:** Domain name server record. If you need to delegate a subdomain name to another DNS service provider for resolution, you need to add an NS record.
**AAAA record:** Used to specify the IPv6 address (e.g., ff06:0:0:0:0:0:0:c3) corresponding to the hostname (or domain name).
**MX record:** If you need to set up your mailbox so that it can receive mail, you need to add an MX record.

### What are the uses of a line?
A line makes users of the specified line access the specified IP.
Common uses include:
**Default:** It must be added; otherwise, only the specified lines can access your website. If it is to resolve for two lines, it is recommended to enter a **China Telecom IP** for the **Default** line.
**China Unicom:** It separately specifies the server IP for **China Unicom users**, while other users still access the **default** line.
**Search engine:** It specifies a server IP for crawling.

### How to enter a record value?
The most common practice is to enter the **IP address** provided by the host service provider, and the record values of each type are generally like the ones below:
- **A Record:** Enter your server IP; if you don't know it, please consult your host service provider.
- **CNAME record:** Enter the domain name provided by your host service provider, for example, 2.com.
- **MX record:** Enter the IP address of your mail server or the domain name provided by your email service provider. If you don't know it, please consult your email service provider.
- **AAAA record:** Not commonly used. It resolves to an IPv6 address.
- **NS record:** Not commonly used. Please do not modify the two default NS records added by the system. When delegating NS, enter the DNS domain name, for example, ns3.dnsv3.com.
- **TTL:** Time to live of the cache. It refers to the period during which a local DNS server caches your domain name record information. After the cache expires, it will get the record value again from DNSPod. The default value of 600 seconds is the most common value and does not need to be modified.
    * 600 (10 minutes): It is recommended to use 600 under normal conditions.
    * 60 (1 minute): If you change the IP frequently, the modified record will take effect in one minute. If the value of 60 is used for a prolonged period, the resolution speed will be slightly reduced.  
    * 3600 (1 hour): If your IP is rarely changed (only a few times a year), it is recommended to use 3600, and the resolution will be faster. When you want to modify the IP, change the value to 60 one day in advance, so that the modification will take effect quickly.  

### Why do I get a "record conflict" prompt when adding a resolution record?  
Because different types of resolution records have different priorities, there will be a record conflict if different types of resolution record values exist for the same host.
The specific conflicts are as follows:
* A CNAME record conflicts with any other records, but does not conflict with another CNAME record;
* A URL (explicit and implicit) record conflicts with A, CNAME, NS, AAAA, MX and URL records, but does not conflict with other records;
* An A record conflicts with CNAME, NS and URL (explicit and implicit) records, but does not conflict with another A record or other records;
* A TXT record conflicts with CNAME and NS records, but does not conflict with another TXT record or other records;
* An AAAA record conflicts with CNAME, NS, URL (explicit and implicit) records, but does not conflict with another AAAA record or other records;
* An SRV record conflicts with CNAME and NS records, but does not conflict with another SRV record or other records;
* An MX record conflicts with CNAME, NS, URL (explicit and implicit) records, but does not conflict with another MX record or other records;
* An NS record conflicts with any other records, but does not conflict with another NS record.

### What should I do if I am prompted that "System busy. Please try again later" when adding a record in Tencent Cloud DNS?
* This error may occur if your domain name resolution already exists. You can log in to the Tencent Cloud **[Console](https://console.cloud.tencent.com/)**, go to **Cloud Products** > **Domain Name Management** and click **Resolution** in the domain name list for search.  
* If you do not find it in the domain name management console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


### My domain name is purchased at Wanwang and resolved at Tencent Cloud DNS with an A record. The console displays that an A record has already been added, but the domain name cannot be resolved. Why?
After adding the domain name in Tencent Cloud DNS, you need to first go to Wanwang to change the DNS address to the `f1g1ns1.dnspod.net f1g1ns2.dnspod.net` and then add the record. Otherwise, Wanwang's DNS addresses conflict with those of Tencent Cloud DNS, which will lead to wrong resolution, and the added record will not work.

