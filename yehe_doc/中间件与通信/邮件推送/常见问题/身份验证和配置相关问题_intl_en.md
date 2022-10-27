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
- `sampledomain.com` is a sample only and should be replaced with your sender domain.
- A domain in the `sampledomain.com` format is a primary domain, and one in the `abc.sampledomail.com` format is a non-primary domain. The following configuration steps vary depending on the domain type (primary or non-primary). See the corresponding description for details.
</dx-alert>
3. Go back to the [Sender Domain](https://console.cloud.tencent.com/ses/domain) page and click **Verify**.
![](https://qcloudimg.tencent-cloud.cn/raw/305ea2b8c9b3c5f10e0dbbe6135b3666.png)
4. Record the `Record Value` shown on the pop-up window.[](id:step4)
>? Below is an example only. The actual content displayed on the corresponding page shall prevail.
>
![](https://qcloudimg.tencent-cloud.cn/raw/70bfe55a17122848c7f829c5b4b86653.png)
5. If your domain is hosted with Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure verification information. Click a sender domain to go to the configuration page.
<dx-alert infotype="explain" title="">
If your domain is hosted with another domain service provider, configure it as instructed in the checklist.
</dx-alert>
6. Take the primary domain `sampledomain.com` as an example to add records. Fill in `Record Value` obtained in the above [step 4](#step4).
  - MX authentication
    Host record: `@`
    Record type: MX
    Record value: `mxbiz1.qq.com.` If you have an email server, enter your email server address in the record value.
<dx-alert infotype="explain" title="">
- For a non-primary domain, `abc.sampledomain.com`, for example, the host record should be `abc`.
- Make sure the record value is ended with `.` Some domain service providers add the `.` at the end of an MX record by default.
</dx-alert>
  - SPF authentication
  Host record: `@`
  Record type: TXT
  Record value: `v=spf1 include:qcloudmail.com ~all`
<dx-alert infotype="explain" title="">
- For a non-primary domain, `abc.sampledomain.com`, for example, the host record should be `abc`.
- If you have multiple email push service providers, you need to include domains of all these service provides in the record value, `v=spf1 include:qcloudmail.com include:domain1.com ~all`, for example, where `domain1.com` represents the domain of another email push service provider. Make sure that there is only one SPF record in the DNS configuration of your sender domain.
</dx-alert>
  - DKIM authentication:
    Host record: `qcloud._domainkey`
  Record type: TXT
  Record value: Your record value.
<dx-alert infotype="explain" title="">
For a non-primary domain, `abc.sampledomain.com`, for example, the host record should be `qcloud._domainkey.abc`.
</dx-alert>
- DMARC authentication:
  Host record: `_dmarc`
  Record type: TXT
  Record value: `v=DMARC1; p=none`
  <dx-alert infotype="explain" title="">
- For a non-primary domain, `abc.sampledomain.com`, for example, the host record should be `_dmarc.abc`.
- The DMARC record must contain the `v` and `p` flags. If you know more about DMARC, you can add other flags or modify flag values as needed.
</dx-alert>

7. Go back to [step 4](#step4) and click **Submit** for verification. The **Current Value** shows what you configured in the above DNS configuration. When the verification status becomes **Verified**, the configuration is completed.

:::
::: Step 2. Verify the result
<dx-alert infotype="explain" title="">
If the configuration operation in Step 1 is completed and the sender domain is “Verified”, skip this verification step.
</dx-alert>
This document describes how to query the DNS domain server with the dig command and check whether your sender domain is properly set.
Enter the following commands in the command line, respectively, and press the carriage return to check whether the returned values are the same as those displayed on the sender domain configuration page.
- `dig mx +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/76cf66d8a42bee99a696b505eb8d8b2c.png)
- `dig txt +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/f5fe74ee3c0c8312253359f8a3457db1.png)
- `dig txt +short _dmarc.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/2c53ae3c3789e220e7f939be536152bf.png)
- `dig txt +short qcloud._domainkey.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/5c773b8278d5d424a652b396f42fc591.png)


<dx-alert infotype="explain" title="">
`sampledomain.com` in the above commands is a sample only and should be replaced with your sender domain.
</dx-alert>




:::
</dx-tabs>

<dx-alert infotype="explain" title="">

- If there is any issue after you perform configuration and verification as described above, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- If you have used the DNSPod service, but it cannot be found by the dig command, the identity verification for the domain may have failed (so the registry stopped resolution).
</dx-alert>
