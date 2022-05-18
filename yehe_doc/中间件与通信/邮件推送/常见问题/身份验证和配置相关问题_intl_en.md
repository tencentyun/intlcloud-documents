[](id:que1) 

### What authentication mechanisms does SES support?
SES supports all industry-standard authentication mechanisms, including DomainKeys Identified Mail (DKIM), Sender Policy Framework (SPF), Domain-Based Message Authentication, Reporting and Conformance (DMARC), and Mail Exchanger (MX) Record.

[](id:que2) 
### How do I configure a sender domain?
<dx-tabs>
::: Step 1. Configure the DNS

1. Click **Create** on the [Sender Domain](https://console.cloud.tencent.com/ses/domain) page.
![](https://qcloudimg.tencent-cloud.cn/raw/57ab829c645dcb868dbb1643ffc3378d.png)
2. Enter a domain and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/43d669f7d15b74bd3f1d11dd3c61d969.png)
<dx-alert infotype="explain" title="">
- `sampledomain.com` is a sample only and should be replaced with your sender address.
- A domain in the `sampledomain.com` format is a primary domain, and one in the `abc.sampledomail.com` format is a non-primary domain. The following configuration steps vary depending on the domain type (primary or non-primary). See the corresponding description for details.
</dx-alert>
3. Go back to the [Sender Domain](https://console.cloud.tencent.com/ses/domain) page and click **Verify**.
![](https://qcloudimg.tencent-cloud.cn/raw/305ea2b8c9b3c5f10e0dbbe6135b3666.png)
4. Record the `Record Value` shown on the pop-up window.[](id:step4)
<dx-alert infotype="explain" title="">The contents in the following figure are samples only. Those on your page shall prevail.</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/70bfe55a17122848c7f829c5b4b86653.png)
5. If your domain is hosted with Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure verification information. You can click a sender domain to go to the configuration page.
<dx-alert infotype="explain" title="">
If your domain is hosted with another domain service provider, configure it as instructed in the checklist.
</dx-alert>
6. Take the primary domain `sampledomain.com` as an example to add records. Fill in `Record Value` obtained in the above [step 4](#step4).
  - MX authentication
    Host record: `@`
    Record type: MX
    Record value: `mxbiz1.qq.com.`
<dx-alert infotype="explain" title="">
- For a non-primary domain, for example, `abc.sampledomain.com`, the Host record should be `abc`.
- Make sure the record value is ended with `.` Some domain service providers add the `.` at the end of a MX record by default.
</dx-alert>
  - SPF authentication
  Host record: `@`
  Record type: TXT
  Record value: Your record value.
<dx-alert infotype="explain" title="">
- For a non-primary domain, for example, `abc.sampledomain.com`, the Host record should be `abc`.
- If you have multiple email push service providers, you need to include domains of all these service provides in the record value, for example, `include:qcloudmail.com include:domain1.com`, where `domain1.com` represents the domain of another email push service provider.
</dx-alert>
  - For DKIM authentication, two records are required:
    - Host record: `mail._domainkey`
  Record type: TXT
  Record value: Your record value.
<dx-alert infotype="explain" title="">
For a non-primary domain, for example, `abc.sampledomain.com`, the Host record should be `mail._domainkey.abc`.
</dx-alert>
- Host record: `qcloud._domainkey`
    Record type: TXT
  Record value: Your record value.
  <dx-alert infotype="explain" title="">
For a non-primary domain, for example, `abc.sampledomain.com`, the Host record should be `qcloud._domainkey.abc`.
</dx-alert>
- DMARC authentication:
Host record: `_dmarc`
  Record type: TXT
  Record value: `v=DMARC1; p=none; rua=mailto:dmarc_report@xxx.com; ruf=mailto:dmarc_report@xxx.com; adkim=r; aspf=r`
  <dx-alert infotype="explain" title="">
- For a non-primary domain, for example, `abc.sampledomain.com`, the Host record should be `_dmarc.abc`.
- `dmarc_report@xxx.com` in the record value is a sample only and should be replaced with an email address that can receive email spoofing reports.
</dx-alert>

7. Go back to [Sender Domain](https://console.cloud.tencent.com/ses/domain) page and click **Verify**. `Current Value` shows the content you set in the above domain verification configuration steps. If `Record Value` and `Current Value` are identical, the verification status will become `verified`, indicating successful configuration.

:::
::: Step 2. Verify the result
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)
:::
</dx-tabs>

<dx-alert infotype="explain" title="">
- If there is any issue after you perform configuration and verification as described above, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- If you have used the DNSPod DNS resolution, but it cannot be found by the `dig` command, the identity verification for the domain may have failed (so the registry stopped resolution).
</dx-alert>

