### 1. What is HTTPS?
HTTPS refers to Hypertext Transfer Protocol Secure, which is a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide the certificate for the domain name and deploy it on the CDN nodes across the network to implement the encrypted data transfer across the network.

### 2. Does CDN support HTTPS configuration?
Tencent Cloud CDN fully supports HTTPS configuration. You can either upload your own certificate for deployment or go to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) to apply for a third party certificate that is provided by TrustAsia free of charge.

### 3. How to configure HTTPS certificate?
You can configure the HTTPS certificate in the CDN Console. For more information, see [HTTPS Configuration](https://intl.cloud.tencent.com/document/product/228/6295).

### 4. Do the HTTPS certificates on CDN nodes need to be synchronized with the updates of HTTPS certificate on origin server?
This depends on your origin-pull method.
HTTP Forwarding: Synchronization is not needed.
HTTPS Forwarding: When the certificate on origin server is updated, the certificates on the CDN nodes need to be updated synchronously. The certificate between client and node must be identical to the one between node and origin server. Otherwise, a failure of origin-pull will occur.

### 5. Is there any way for users to allow only HTTPS access and forbid HTTP access?
You can use Forced HTTPS Redirection. After the certificate is configured successfully, the **Forced Redirect** option appears. When it’s enabled, even if you initiate an HTTP request, it will be changed to an HTTPS request.
![](https://main.qcloudimg.com/raw/0352df67305e2e7f4c6df51b0b1afc09.png)
