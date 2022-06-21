### Reverse DNS Overview
Reverse DNS resolves an IP address back to a domain, as opposed to forward DNS that maps a domain to an IP address.

An IP may be used by multiple domains, and it is necessary to verify if this is the case before reverse DNS is carried out. It will be impossible to start from the IP to traverse the entire DNS system for verification due to the massive amount of engineering work. Therefore, RFC 1035 defines a pointer (PTR) record to point an IP address to a domain.
>? Private DNS refers to the resolution of domains in a private network, while Public DNS is oriented to internet users. Reverse DNS can be carried out in a public or private network, and the definitions and features involved are consistent in both cases.


### Adding a PTR Record

Before adding a PTR record, you must create a reverse private domain of the IP range first.

1. If your IP range is `192.168.0.1`–`192.168.0.255` and the class C IP is `192.168.0.1/24`, the reverse private domain corresponding to the IP range is `0.168.192.in-addr.arpa`.
2. When you add the private domain `0.168.192.in-addr.arpa` in Private DNS and add the PTR record with the host as `1` pointing to `www.dnspod.com`, the reverse DNS of the IP address `192.168.0.1` is `www.dnspod.com`.

>? The prefix of the combination of the host and the private domain (the prefix of `in-addr.arpa`) must comply with the IPV4 format specification. For example, to create a private domain `10.255.123.in-addr.arpa`, the host can only be an integer between 0 and 255.

### Adding Reverse Private Domain
The following steps take the reverse private domain `0.168.192.in-addr.arpa` as an example.

1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/domains).
2. On the **Private Domain List** page, click **Create Private Domain**.
3. On the **Create Private Domain** page, enter the reverse DNS domain and select a VPC.
For example, enter `0.168.192.in-addr.arpa` as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/30fe057332d414f15163c18e56a6f19d.png)
>?
>- For a better experience, we recommend you create a private domain and set a DNS record for it first before associating a VPC.
>- If no VPCs are displayed for the currently selected region, create one in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- If existing VPCs cannot meet your needs, you can modify them in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- VPC regions currently available for association include Beijing, Shanghai, Chengdu, Chongqing, Guangzhou, and Silicon Valley.
4. Click **Confirm** to add the reverse private domain. You can directly enter the DNS records page of the domain to add a PTR record as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/724f6ca08c314bb110693797827372df.png)


### Private IP Range
On the public network, reverse DNS cannot be provided by DNS service providers, because the management permissions of IP addresses are owned by ISPs. Therefore, it is necessary to apply to ISPs for adding reverse DNS records.

However, things are different in **VPC**. **You can use any of the following private IP ranges as your VPC IP range**:

```
`10.0.0.0` - `10.255.255.255` (mask range: 16 to 28)
`172.16.0.0` - `172.31.255.255` (mask range: 16 to 28)
`192.168.0.0` - `192.168.255.255` (mask range: 16 to 28)
```

Correspondingly, you can also create reverse private domains within these three IP ranges.

>?
>- For more information about private IP ranges, see [Network Planning](https://intl.cloud.tencent.com/document/product/215/31795).
>- Reverse domains of the same IP range are regarded as the same private domains, which cannot be associated with the same VPC; for example, `2.1.in-addr.arpa` and `4.3.1.in-addr.arpa` cannot be associated with the same VPC.
>- For more information on how to add PTR records in Private DNS, see [PTR Record](https://intl.cloud.tencent.com/document/product/1097/40573).





