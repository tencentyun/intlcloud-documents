[](id:que1) 

### What authentication mechanisms does SES support?
SES supports all industry-standard authentication mechanisms, including DomainKeys Identified Mail (DKIM), Sender Policy Framework (SPF), and Domain-Based Message Authentication, Reporting and Conformance (DMARC).

[](id:que2) 
### How do I configure a sender domain?
<dx-tabs>
::: Step 1. Configure on the DNS page
1. On the [Sender Domain](https://console.cloud.tencent.com/ses/domain) configuration page, click **Create**, enter the domain name, and submit.
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. Configure the verification information in the [DNSPod console](https://console.cloud.tencent.com/cns).
3. [](id:step2)Return to the [Sender Domain](https://console.cloud.tencent.com/ses/domain) configuration page and click **Verify**.
4. Click the sender domain address to enter the configuration details page, where you can see the domain value.
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
5. Paste the sender domain address in [step 3](#step3) to the [DNSPod](https://console.cloud.tencent.com/cns) page to add a record. Be sure to avoid spaces.
 - DKIM authentication:
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - SPF authentication:
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - _dmarc record:
Enter `v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;` as the record value.
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
6. Go back to the [Sender Domain](https://console.cloud.tencent.com/ses/domain) configuration details page and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: Step 2. Verify the result
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: Supplement: when the sender domain is a third-level domain
1. On the [Sender Domain](https://console.cloud.tencent.com/ses/domain) configuration page, click **Create**, enter the domain name, and submit.
2. Configure the verification information in the [DNSPod console](https://console.cloud.tencent.com/cns).
:::
</dx-tabs>

>?
>- After the above configuration and verification, if the issue persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>- If the DNSPod resolution is registered, but it cannot be found by the `dig` command, the reason may be that identity verification has not been completed for the domain (so the registry stopped resolution).
