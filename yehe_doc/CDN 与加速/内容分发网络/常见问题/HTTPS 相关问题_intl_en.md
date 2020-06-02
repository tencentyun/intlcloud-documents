### What is HTTPS?
HTTPS refers to Hypertext Transfer Protocol Secure, a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all CDN nodes to implement encrypted data transfer across the entire network.

### Does CDN support HTTPS configuration?
Yes. Tencent Cloud CDN fully supports HTTPS configuration. You can either upload your own certificate for deployment or go to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) to apply for a free third-party certificate provided by TrustAsia.

### How do I configure a HTTPS certificate?
You can configure a HTTPS certificate on the CDN Console. For more information, please see [HTTPS Acceleration Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).

### Do the HTTPS certificates on CDN nodes need to be synced with HTTPS certificate updates on the origin server?
This depends on your origin-pull method.
HTTP forwarding: they do not need to be synced.
HTTPS forwarding: when the certificate on the origin server is updated, the certificates on the CDN nodes need to be updated synchronously. The certificate between the client and the node must be identical to the one between the node and the origin server. Otherwise, origin-pull will fail.

### Is there any way for users to allow only HTTPS access and forbid HTTP access?
Yes. You can use the forced HTTPS redirection feature. After the certificate is configured successfully, the "Forced Redirect to HTTPS" switch will appear. When it is enabled, even if a user initiates a HTTP request, the request will be redirected to a HTTPS request for access.
![](https://main.qcloudimg.com/raw/f3b267f6140375bb728418f9b29026d8.png)


### Why does HTTPS access not work after CDN is configured?

You need to upload the website's HTTPS certificate to CDN using the following steps:
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to access the domain name management page. Click **Manage** on the right of the domain name to access the management page.
![](https://main.qcloudimg.com/raw/518644b104972679d063ec3bb790ea31.png)
2. Click **Advanced Configuration** and find the HTTPS configuration module. Click **Configure Now** to access the certificate management page and configure a certificate. For the configuration steps, please see [HTTPS Acceleration Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213#.E5.9F.9F.E5.90.8D.E9.85.8D.E7.BD.AE). ![](https://main.qcloudimg.com/raw/49ed20144b4018164794926576a26c1c.png)
3. After the certificate is configured successfully, the **Forced Redirect to HTTPS** switch will appear. When it is enabled, even if a user initiates a HTTP request, the request will be redirected to a HTTPS request for access.
![](https://main.qcloudimg.com/raw/98993eaa23a524bcc2cb8a168fbaccd3.png)



