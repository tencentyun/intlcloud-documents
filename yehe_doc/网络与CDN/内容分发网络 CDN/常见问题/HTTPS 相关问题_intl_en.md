[](id:q1)
### What is HTTPS?
HTTPS refers to Hypertext Transfer Protocol Secure, a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all CDN nodes to implement encrypted data transfer across the entire network.

[](id:q2)
### Does CDN support HTTPS configuration?
Yes. Tencent Cloud CDN fully supports HTTPS configuration. You can either upload your own certificate for deployment or go to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) to apply for a free third-party certificate provided by TrustAsia.

[](id:q3)
### How do I configure an HTTPS certificate?
You can configure an HTTPS certificate in the [CDN console](https://console.cloud.tencent.com/cdn). For detailed directions, please see [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).

[](id:q4)
### Do the HTTPS certificates on CDN nodes need to be synchronized with HTTPS certificate updates on the origin server?
No. Updating the HTTPS certificate of your origin server does not affect the one configured on CDN. You only need to update the HTTPS certificate on CDN when it is or about to be expired.


[](id:q5)
### Can I deny HTTP access and allow HTTPS access only?
Yes. After successfully configuring an HTTPS certificate, you can use the [Forced Redirection](https://intl.cloud.tencent.com/document/product/228/35214) feature. HTTP requests from users will be forcibly redirected to HTTPS requests.
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### Why does HTTPS access not work after CDN is configured?

For HTTPS access, please configure it as instructed:
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its management page.
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2. Open the **Advanced Configuration** tab to find the **HTTPS Configuration** section, and click **Configure Now** to go to the **Certificate Management** page. For configuration directions, please see [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE).
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
HTTPS access can be enabled after the certificate is successfully configured.



