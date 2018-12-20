### What is reverse resolution?
Reverse domain name resolution is the process of mapping from IP address to domain name. Since forward resolution is the process of mapping from domain name to IP address, if you want to know whether an IP address corresponds to one or more domain names, you need to traverse the entire domain name system, which is simply impossible. Therefore, RFC1035 defines a PTR (pointer) record as a data type in the mailbox system. In contrast to an A record, a PTR record points an IP address to a domain name.
### In what scenarios can I use reverse resolution?
Reverse resolution should mainly be used in mail servers. After it is enabled, messages sent from IPs with no domain names registered can be rejected. As most spammers use dynamically assigned IPs or IPs with no domain names registered to send spams while stay anonymous, spams can be prevented by rejecting messages in the mail server from IP addresses that cannot be reversely resolved to domain names.
### How does Tencent Cloud achieve reverse resolution?
As shown above, reverse resolution cannot be completed by the DNS service provider. Instead, it is required to be applied for to the ISP. Therefore, Tencent Cloud only supports reverse resolution for IP addresses that are Tencent Cloud resources. Currently, this feature is available to organizational VIP customers. If you need it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=16&level2_id=17&level1_name=%E5%85%B6%E4%BB%96%E6%9C%8D%E5%8A%A1&level2_name=%E5%9F%9F%E5%90%8D) for approval.
Other developers are recommended to use third-party corporate email services.

>**Note:**
>When submitting the ticket, please detail your domain names and public IPs (which are Tencent Cloud resources).
