### Reverse DNS Overview
Reverse DNS maps IP address to domain name, as opposed to forward DNS that maps domain name to IP address.

As an IP may be used by multiple domain names, it is necessary to verify whether the IP address corresponds to one or more domain names before performing reverse DNS. It will be impossible to start from the IP to traverse the entire DNS system for verification due to the massive amount of work. Therefore, RFC 1035 defines a pointer (PTR) record to point an IP to a domain.

### Adding PTR Record

Before adding a PTR record, you must create a reverse private domain of the IP range first.

1. If your IP range is `192.168.0.1`–`192.168.0.255` and the class C IP `192.168.0.1/24`, then the reverse private domain corresponding to the IP range is `0.168.192.in-addr.arpa`.
2. When you add the private domain `0.168.192.in-addr.arpa` in Private DNS and add the PTR record with the host as `1` pointing to `www.dnspod.com`, the reverse DNS result of the IP address `192.168.0.1` is `www.dnspod.com`.

>?The prefix of the combination of the host and the private domain (i.e., the prefix of `in-addr.arpa`) must comply with the IPv4 format specification. For example, to create a private domain of `10.255.123.in-addr.arpa`, the host can only be an integer between 0 and 255.

### Adding Reverse Private Domain
The following steps take the reverse private domain `0.168.192.in-addr.arpa` as an example.

1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/domains).
2. In the **Private Domain List**, click **Create Private Domain** as shown below:
![](https://main.qcloudimg.com/raw/e453ae30a0ae9aa0618be2e01404aeca.png)
3. On the **Create Private Domain** page, enter the reverse DNS domain name and select a VPC.
For example, enter `0.168.192.in-addr.arpa` as shown below:
![](https://main.qcloudimg.com/raw/3c8b0405e91b4ca8aafd0150c7da0adb.png)
>?
>- For a better experience, we recommend you create a private domain name and set a DNS record for it first before associating a VPC.
>- If no VPCs are displayed in the currently selected region, please create one in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- If existing VPCs cannot meet your needs, you can modify them in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1/).
>- VPC regions currently supported for association include Beijing, Shanghai, Chengdu, Chongqing, Guangzhou, and Silicon Valley.
4. Click **Confirm** to add the reverse private domain. You can directly enter the DNS records page of the domain to add a PTR record as shown below:
![](https://main.qcloudimg.com/raw/9a211374713ea4b8188da47ae50dad86.png)


### Private IP Range
On the public network, reverse DNS cannot be provided by DNS service providers, as the management permissions of IP addresses are owned by ISPs. Therefore, it is necessary to apply to ISPs for adding reverse DNS records.

However, things are different in **VPC**. **You can use any of the following private IP ranges as your VPC IP range**:

```
10.0.0.0–10.255.255.255 (the mask range should be between 16 and 28)
172.16.0.0–172.31.255.255 (the mask range should be between 16 and 28)
192.168.0.0-192.168.255.255 (the mask range should be between 16 and 28)
```

You can also create reverse private domains within these three IP ranges.

>?
>- For more information on private IP ranges, please see [Network Planning](https://intl.cloud.tencent.com/document/product/215/31795).
>- Reverse domain names of the same IP range are regarded as the same private domains, which cannot be associated with the same VPC; for example, `2.1.in-addr.arpa` and `4.3.1.in-addr.arpa` cannot be associated with the same VPC.
>- For more information on how to add PTR records in Private DNS, please see [PTR Record](https://intl.cloud.tencent.com/document/product/1097/40573).




